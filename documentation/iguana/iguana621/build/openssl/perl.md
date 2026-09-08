# Perl

The simplest most deterministic way I could think of installing the perl dependency on windows is something like this:

The logic behind this approach is to **avoid modifying the global environment of the machine** by using a *portable* version of Strawberry Perl. Instead of running a system-wide installer that could change PATH variables or overwrite existing Perl configurations, this method simply downloads and unpacks Perl into a local directory within your project. This keeps your dependency isolated—**changes are only within your project folder**—and ensures no risk to other applications or system settings.

By simplifying and isolating the environment in this way, you **avoid risk and make the build process deterministic and reproducible**. Anyone building your project will get the exact Perl version required, with no side effects, simply by running `make`. No need for administrator rights or manual cleanup, and if you want to remove it, you just delete the project folder—*nothing spills into the wider system*

```
EliotHomeServer:~/builds/iguana6/openssl_perl % make
curl -L "https://strawberryperl.com/download/5.20.3.3/strawberry-perl-5.20.3.3-64bit-portable.zip" -o "strawberry-perl-5.20.3.3-64bit-portable.zip"
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  110M  100  110M    0     0  4304k      0  0:00:26  0:00:26 --:--:-- 3424k
mkdir install
tar -xf "strawberry-perl-5.20.3.3-64bit-portable.zip" -C install
echo installed > "./install/perl.installed"
EliotHomeServer:~/builds/iguana6/openssl_perl % make
make: Nothing to be done for `all'.
```
