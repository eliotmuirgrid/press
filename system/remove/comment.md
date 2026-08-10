# Comment

**Removing comments from code actually makes it simpler and faster for both machines and humans to read.**

I discovered this while contemplating [separating functions](/system/separate/function).

Initially, I attempted to write parsing code to identify the functions in a C++ file. However, I soon realized that the problem became infinitely more straightforward if we could assume there were no comments present. In this scenario, you wouldn't have to worry about `{` and `(` characters that had been commented out and should be excluded from the parse.

Contrary to what Chat GPT initially suggested, preserving comments is not a good idea. By doing so, you'd have two sources of truth: the comment's intent and the code itself. Only one truth matters: what the code actually does, not what the intent of the code author is.

The main issue with commenting code manually is that it introduces inconsistencies between the intended behavior (in the comments) and what the code actually does. This can lead to maintenance issues down the line, as you'll need to reconcile these [two sources of truth](/system/two/truth).

>Only one truth matters.  What the code actually does.  Not what the intent of code author is.

I got ChatGPT to produce the first cut of a comment remover.  All well
and good.  It **appeared** to work well - but how do I test it?

Here's the code before:

```
//----------------------------------------------------------------
// Copyright (C) Eliot Muir 2026 All rights reserved.
//
// Implementation
//
// Date: Wednesday 29th July 2026
//       0x6A6A23C9 seconds since the beginning of the Unix Epoch time
//       The dawn of our new age. 
// ---------------------------------------------------------------


#include "FILdirSeparator.h"
#include "COLtrace.h"
COL_TRACE_INIT;

#define MAX_NESTED_DEPTH 256

static bool FILisThisAlpha(const char C){
   return ((0x41 <= C && C <= 0x5a) || (0x61 <= C && C <= 0x7A));
}

static bool FILcheckDirDepthLimit(int DirectoryDepth){
   // COL_FUNCTION(FILcheckDirDepthLimit);      
   if (DirectoryDepth >= MAX_NESTED_DEPTH){                     
      COL_TRC("Directory depth exceeds 256");
      return false;                      
   } else if (DirectoryDepth < 0){
      COL_TRC("Directory depth below 0");
      return false;
   }                 
   return true;              
}

bool FILpathSimplify(COLstring* pPath) {
   COL_FUNCTION(FILpathSimplify);
   COLstring& Path = *pPath;
   COL_VAR(Path);
   // This function will attempt to 'simplify' a path via the following methods:
   //   * Stripping out any './' which exist
   //   * Removing any '../' which are resolveable
   //   * Removing any extraneous slashes (i.e. 'foo//bar')
   //
   // The algorithm itself is pretty much what would happen if you did it by
   // hand. It works its way through the string, and instead of using substring
   // to cut out extraneous directories, it just moves the write pointer back 
   // and overwrites them. 

   const char* pInput = Path.data();

   // This holds our output. It must be big enough for us to have the entire 
   // Path in it, and pre-allocating means we can pretty much treat it as
   // a big block of data.
   COLstring Buffer;
   Buffer.setCapacity(Path.size() + 1);

   char* pOutputStart = Buffer.data();

   // This is our actual write pointer, which we move around as we pass over
   // the input.
   char* pOutput = pOutputStart;

   // Our stack of directories, which are just pointers within the output
   // Buffer.
   char* pDirectoryOffsets[MAX_NESTED_DEPTH];

   // How many directories are in the directory stack.
   int DirectoryDepth = 0;

   // The separator we wish to use. This code will use the 'proper' separators
   // when it identifies a Windows, *NIX or Samba absolute path, otherwise it 
   // uses the system default.
   char Separator = FILdirSeparator[0];

   enum {
      ST_START,  // Beginning of a directory name, we're at the first char after the slash.
      ST_DATA,   // Any old directory name content which isn't something we specifically care about.
      ST_DOT,    // We've seen a single . at the start of a dir name so far
      ST_DOTDOT  // Two dots!
   } State = ST_START;

   // Figure out what kind of path we're dealing with here
   if (Path.size() >= 1 && 
       *pInput == '/')
   {
      COL_TRC("POSIX style absolute path.");
      // POSIX-style absolute path
      Separator = '/';
      *pOutput++ = *pInput++;
   }
   else if (Path.size() >= 2 &&
            ::memcmp(pInput, "\\\\", 2) == 0)
   {
      COL_TRC("Samba style absolute path.");
      // Samba-style absolute path
      Separator = '\\';
      ::memcpy(pOutput, pInput, 2);
      pOutput += 2;
      pInput += 2;
   }
   else if (Path.size() >= 3 && 
            FILisThisAlpha(pInput[0]) &&
            pInput[1]==':' &&
            (pInput[2]=='/' || pInput[2]=='\\')
         )
   {
      COL_TRC("Windows style absolute path.");
      // Windows-style absolute path
      Separator = '\\';
      pOutput[0] = pInput[0];
      pOutput[1] = pInput[1];
      pOutput[2] = Separator;
      //::memcpy(pOutput, pInput, 3);
      pOutput += 3;
      pInput += 3;
   }
   else
   {
      COL_TRC("Relative path.");
      // Relative path of some sort, we use the current platform's default
      // separator.
   }

   // Set up where our 'root' directory is.
   pDirectoryOffsets[DirectoryDepth++] = pOutput;

   while (*pInput)
   {
      // LastChar is the value we've seen. We move the pointers ahead before
      // we look at its value for non-separator cases, so it's more sane to 
      // have it in a variable.
      char LastChar = *pInput;
      switch (LastChar)
      {
         case '\\':
         case '/':
            LastChar = Separator;
            break;
         default:
            break;
      }

      pInput++;
      *pOutput++ = LastChar;

      switch (State)
      {
         case ST_START:
            switch (LastChar)
            {
               case '.':
                  State = ST_DOT;
                  break;
               case '\\':
               case '/':
                  // Since we're at the start of a directory name, this means 
                  // that we have multiple slashes, which are redundant and can
                  // be stripped out.
                  pOutput--;
                  State = ST_START;
                  break;
               default:
                  State = ST_DATA;
                  break;
            }
            break;
         case ST_DATA:
            switch (LastChar)
            {
               case '\\':
               case '/':
                  // We've got a non-special directory name, so we just keep
                  // going after adding our write position to the stack.
                  State = ST_START;
                  if (!FILcheckDirDepthLimit(DirectoryDepth)) { return false; }  // IX-4181 
                  pDirectoryOffsets[DirectoryDepth++] = pOutput;
                  break;
               default:
                  break;
            }
            break;
         case ST_DOT:
            switch (LastChar)
            {
               case '\\':
               case '/':
                  // We've seen a reference to the current directory, so we 
                  // rewind to the character after the previous slash.
                  if (!FILcheckDirDepthLimit(DirectoryDepth)) { return false; } // IX-4181
                  pOutput = pDirectoryOffsets[DirectoryDepth - 1];
                  State = ST_START;
                  break;
               case '.':
                  State = ST_DOTDOT;
                  break;
               default:
                  State = ST_DATA;
                  break;
            }
            break;
         case ST_DOTDOT:
            switch (LastChar)
            {
               case '\\':
               case '/':
                  // We've seen a reference to the parent directory. Make sure
                  // that we have enough directories to be able to resolve the
                  // parent and back ourselves up.
                  if (DirectoryDepth >= 2)
                  {
                     pOutput = pDirectoryOffsets[(--DirectoryDepth) - 1];
                  }
                  State = ST_START;
                  break;
               default:
                  State = ST_DATA;
                  break;
            }
            break;
      }
   }
   
   // Make sure we handle a .. or . at the end of a string without a trailing
   // slash correctly.
   switch (State)
   {
      case ST_DOT:
         if (!FILcheckDirDepthLimit(DirectoryDepth)) { return false; } // IX-4181
         pOutput = pDirectoryOffsets[--DirectoryDepth];
         break;
      case ST_DOTDOT:
         if (DirectoryDepth >= 2)
         {
            pOutput = pDirectoryOffsets[(--DirectoryDepth) - 1];
         }
         break;
      default:;
   }

   // Not NULL-terminated, use the special constructor.
   COLstring SimplePath(pOutputStart, pOutput - pOutputStart);
   COL_VAR(SimplePath);
   Path = SimplePath; 
   return true;
}
```

and after:

```
#include "FILdirSeparator.h"
#include "COLtrace.h"
COL_TRACE_INIT;
#define MAX_NESTED_DEPTH 256
static bool FILisThisAlpha(const char C){
   return ((0x41 <= C && C <= 0x5a) || (0x61 <= C && C <= 0x7A));
}
static bool FILcheckDirDepthLimit(int DirectoryDepth){
   if (DirectoryDepth >= MAX_NESTED_DEPTH){                     
      COL_TRC("Directory depth exceeds 256");
      return false;                      
   } else if (DirectoryDepth < 0){
      COL_TRC("Directory depth below 0");
      return false;
   }                 
   return true;              
}
bool FILpathSimplify(COLstring* pPath) {
   COL_FUNCTION(FILpathSimplify);
   COLstring& Path = *pPath;
   COL_VAR(Path);
   const char* pInput = Path.data();
   COLstring Buffer;
   Buffer.setCapacity(Path.size() + 1);
   char* pOutputStart = Buffer.data();
   char* pOutput = pOutputStart;
   char* pDirectoryOffsets[MAX_NESTED_DEPTH];
   int DirectoryDepth = 0;
   char Separator = FILdirSeparator[0];
   enum {
      ST_START,  
      ST_DATA,   
      ST_DOT,    
      ST_DOTDOT  
   } State = ST_START;
   if (Path.size() >= 1 && 
       *pInput == '/')
   {
      COL_TRC("POSIX style absolute path.");
      Separator = '/';
      *pOutput++ = *pInput++;
   }
   else if (Path.size() >= 2 &&
            ::memcmp(pInput, "\\\\", 2) == 0)
   {
      COL_TRC("Samba style absolute path.");
      Separator = '\\';
      ::memcpy(pOutput, pInput, 2);
      pOutput += 2;
      pInput += 2;
   }
   else if (Path.size() >= 3 && 
            FILisThisAlpha(pInput[0]) &&
            pInput[1]==':' &&
            (pInput[2]=='/' || pInput[2]=='\\')
         )
   {
      COL_TRC("Windows style absolute path.");
      Separator = '\\';
      pOutput[0] = pInput[0];
      pOutput[1] = pInput[1];
      pOutput[2] = Separator;
      pOutput += 3;
      pInput += 3;
   }
   else
   {
      COL_TRC("Relative path.");
   }
   pDirectoryOffsets[DirectoryDepth++] = pOutput;
   while (*pInput)
   {
      char LastChar = *pInput;
      switch (LastChar)
      {
         case '\\':
         case '/':
            LastChar = Separator;
            break;
         default:
            break;
      }
      pInput++;
      *pOutput++ = LastChar;
      switch (State)
      {
         case ST_START:
            switch (LastChar)
            {
               case '.':
                  State = ST_DOT;
                  break;
               case '\\':
               case '/':
                  pOutput--;
                  State = ST_START;
                  break;
               default:
                  State = ST_DATA;
                  break;
            }
            break;
         case ST_DATA:
            switch (LastChar)
            {
               case '\\':
               case '/':
                  State = ST_START;
                  if (!FILcheckDirDepthLimit(DirectoryDepth)) { return false; }  
                  pDirectoryOffsets[DirectoryDepth++] = pOutput;
                  break;
               default:
                  break;
            }
            break;
         case ST_DOT:
            switch (LastChar)
            {
               case '\\':
               case '/':
                  if (!FILcheckDirDepthLimit(DirectoryDepth)) { return false; } 
                  pOutput = pDirectoryOffsets[DirectoryDepth - 1];
                  State = ST_START;
                  break;
               case '.':
                  State = ST_DOTDOT;
                  break;
               default:
                  State = ST_DATA;
                  break;
            }
            break;
         case ST_DOTDOT:
            switch (LastChar)
            {
               case '\\':
               case '/':
                  if (DirectoryDepth >= 2)
                  {
                     pOutput = pDirectoryOffsets[(--DirectoryDepth) - 1];
                  }
                  State = ST_START;
                  break;
               default:
                  State = ST_DATA;
                  break;
            }
            break;
      }
   }
   switch (State)
   {
      case ST_DOT:
         if (!FILcheckDirDepthLimit(DirectoryDepth)) { return false; } 
         pOutput = pDirectoryOffsets[--DirectoryDepth];
         break;
      case ST_DOTDOT:
         if (DirectoryDepth >= 2)
         {
            pOutput = pDirectoryOffsets[(--DirectoryDepth) - 1];
         }
         break;
      default:;
   }
   COLstring SimplePath(pOutputStart, pOutput - pOutputStart);
   COL_VAR(SimplePath);
   Path = SimplePath; 
   return true;
}
```

When I look at code with less interesting thoughts from the author showing his wisdom I notice more interesting things that show his stupidity.

Like WTF - why have a C array.  That's dangerous.  The programmer who wrote this took corners and didn't bother changing the code base over to use it.  Awesome.  I have to fix this code.  I never trust code from anyone.  

The formatting of this code is stupid.  It has a low signal to noise ratio.  I will compact
the code to make it easier to read and reason about.

It's too long.

Funny that this code is vulnerable to a timing attack.  A really sophisticated attacker could in theory deduce interesting information about the file system looking at the timing of the code.  Real security will need to go so deep into hardware that it isn't funny.

Security is very very hard.  There is no way it can be achieved with out a system as
rigorous as what [Flow](/flow) will methodically become.  It will take one insanely committed
programmer to make it happen.

That programmer is Eliot Muir.
