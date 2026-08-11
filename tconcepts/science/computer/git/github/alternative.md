# Alternative


1. **Easily exchanging changes with another user (syncing, sharing, fetching, pushing)**
2. **Easily browsing changes (history, diffs, code navigation, review, discussion)**

A lot of tutorials and articles focus on stuff like “GitHub is for hosting code”, but that misses the real engineering problems underneath.

Let’s go into these two, and what it takes to solve them *without* GitHub, and why GitHub is so sticky:

---

## 1. **Easily Exchanging Changes with Another User**

### The pain:
- With plain Git, you need both sides to have *network access*, some shared point, or to exchange files manually.
- **“Push” and “pull”** are easy if you have a **shared remote** (like a GitHub repo) — otherwise you need a central server, or to set up peer-to-peer access with proper authentication and permissions.
- Without GitHub (or something like it), you have to manually **set up an SSH server, HTTP server, or use a USB stick, email, etc.** This is a pain to automate, secure, or scale across many people.

### Peer-to-peer?
- There’s nothing in Git that requires a central server — you can push/pull between any repos, even “git bundle” files over email.
- But, in practice, people need a *stable point online*, some “single source of truth,” for ease and reliability.
- Peer-to-peer alternatives (like [Radicle](https://radicle.xyz/)) exist, but aren’t as widely adopted as client-server-and-forget.

### In short:
- **Running your own server:** You can run Gitea, GitLab, cgit, etc. on your own box, but now you’re the system admin. You handle backups, authentication, security patches.
- **Peer-to-peer:** Very niche, unusual, and needs all collaborators to be online at the right time or to exchange patches manually.
- **GitHub solves this** by giving a canonical “remote” that’s always up, always available, and easy to connect to.

---

## 2. **Easily Browsing Changes**

### The pain:
- Viewing code history, diffs, and annotations in “raw” Git is possible (`git log`, `git diff`, etc.), but *hard to browse, search, or share*.
- There’s no built-in web GUI. To see code online, you need a web server running a code browser (cgit, Gitea, GitLab, etc.).
- Reviewing changes, sending comments, managing pull-requests — you have to invent your own workflow, or use email patch reviews (time-consuming, lacks UX polish).

### The real value:
- GitHub (and friends) give you an always-on, always-up-to-date, *web-accessible readable* history and review system, visible to anyone you invite.
- This massively flattens the learning-and-collaboration curve, especially for newbies or distributed teams.
- Nothing in “raw” Git gives you good code review threads, change discussions, PR history, search, and so forth.

---

## **Can you exchange and review code changes without GitHub?**

- Absolutely! People used to send `git format-patch` emails, or host public Git servers, or use plain SSH.
- But it’s *much harder* to automate at scale, and teams lose the user interface, shared comments, and notifications that speed up teamwork.

---

## **Summary Table of Realistic Options**

| Problem                                           | “DIY” Solution(s)                                        | GitHub/GitLab/etc Solution   |
|---------------------------------------------------|----------------------------------------------------------|------------------------------|
| Share code changes easily                         | Public git server w/ SSH/HTTP, p2p protocols, email      | Just use “push” to remote    |
| Browse/view code and history                      | Run a web Git viewer (e.g. cgit, Gitea, GitLab)          | Browse on web instantly      |
| Review/discuss/approve changes                    | Email patches; in-person meeting; home-grown workflow     | Pull requests, comments, etc |
| Notifications, visibility, user management        | Custom scripts, mailing lists, manual user handling       | Web UI, automated            |

---

## **Do You *Need* GitHub?**

- **NO. You absolutely do not need GitHub or any cloud service.**
- But you *do* need:
   - Some shared mechanism for code exchange and review
   - Some way to let others see/browse what’s changing

- If you are a *small, tech-savvy* team, you can run your own infrastructure (Gitea, GitLab, email patches, or even private code shares).
- If you want *turnkey*, *less hassle*, and *massive community/discoverability*, you use GitHub.
- Either way, **Git** is the underlying tool. GitHub is just a convenience layer.

---

## **If you’re looking for minimal or privacy-oriented setups:**

- **Gitea** or **Gogs** for fast, light, self-hosted web GUIs (make sure these fit your threat model/security needs).
- **cgit** for dead-simple, read-only web browsing.
- Email patches for peer-to-peer.
- For small groups, even Dropbox/Nextcloud plus “git bare” repos can work internally.

## Summary

- **You don’t need GitHub, but you do need somewhere/somehow to share and review code.**
- Without a platform like GitHub, you’ll need to assemble and run the pieces yourself.
- It’s doable, but a lot more setup and ongoing admin — which is why so many people use GitHub!  Convenience comes at a cost of privacy though.

