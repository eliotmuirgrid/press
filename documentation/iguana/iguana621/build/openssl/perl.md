# Perl

The simplest most deterministic way I could think of installing the perl dependency on windows is something like this:




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
