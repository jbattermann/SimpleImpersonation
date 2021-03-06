SimpleImpersonation
===================

Simple Impersonation Library for .Net

This library provides a managed wrapper for the [LogonUser](http://msdn.microsoft.com/en-us/library/windows/desktop/aa378184.aspx) function of the Win32 API.  Basically, it allows you to impersonate any user, as long as you have their credentials.

It is dual compiled for both .Net 2.0 and .Net 4.0 runtimes.  It should work well under .Net 2.0, 3.0, 3.5, 4.0, 4.5, 4.5.1, 4.5.2, 4.6, and the 4.0 client profiles.  It has no dependencies.

Note that it is *not* compiled for PCL or .NET Core, as it is Windows specific.

Installation
------------

Use NuGet package [SimpleImpersonation](https://nuget.org/packages/SimpleImpersonation/).

```powershell
PM> Install-Package SimpleImpersonation
```

Usage
-----

```csharp
using (Impersonation.LogonUser(domain, username, password, logonType))
{
    // do whatever you want as this user.
}
```

Note: As of version 1.1.0, `password` can be specified as a `SecureString`.  You can still pass a regular `string` if desired, however `SecureString` is recommended.

Be sure to specify a logon type that makes sense for what you are doing.  For example:

- If you are interactively working as a particular user from a desktop application, use `LogonType.Interactive`.

- If you are trying to connect to a SQL server with trusted authentication using specific credentials, use `LogonType.NewCredentials`.
  - But be aware that impersonation is not taken into account in connection pooling.
  - You will also need to vary your connection string.
  - Read more [here](http://stackoverflow.com/q/18198291/634824)



See the [MSDN documentation](http://msdn.microsoft.com/library/windows/desktop/aa378184.aspx) for additional logon types.
