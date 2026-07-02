# NoMAD, Universal — an Apple Silicon fork (2026)

macOS is deprecating Intel-only apps, and the archived upstream only ever shipped Intel builds. The designated successor, [NoMAD-2](https://github.com/jamf/NoMAD-2), never reached a usable state before development stopped — so environments that still rely on NoMAD v1's stability and simplicity were left without a native path forward on Apple Silicon.

This fork takes the archived v1 source and makes it build with current Xcode as a **universal binary (Apple Silicon + Intel)** that runs natively on modern macOS.

**What changed from the archived source:**

- Migrated Swift 3 → Swift 5 (the code hadn't compiled on any Xcode released since ~2017)
- Builds as a universal binary with a native arm64 slice; minimum macOS is now 11.0
- Fixed a launch-sequence hang (`CFRunLoopRun()` in `applicationDidFinishLaunching`) that old macOS tolerated but modern macOS doesn't — it left the menu bar item unclickable and killed the periodic refresh
- Status item ported to the modern `NSStatusItem.button` API so the icon and expiration countdown actually render
- Custom menu bar icons (`IconOn`/`IconOff`/`IconOnDark`/`IconOffDark`) are now rendered as template images, so they adapt to menu bar appearance like a proper status icon

**Building it:** open `NoMAD.xcodeproj` in Xcode and build, or:

```
xcodebuild -project NoMAD.xcodeproj -scheme NoMAD -configuration Release build \
  CODE_SIGN_IDENTITY="-"
```

There are no notarized releases here — it's ad-hoc signed, build-it-yourself. Locally built copies launch without Gatekeeper complaints.

**Caveats:** tested on the maintainer's own machines (macOS 26, Apple Silicon) against a real AD domain — Kerberos sign-in and renewal, password expiration display, keychain integration, and custom icons all verified working. Everything else inherits whatever state the 1.0.5-era code was in. MIT licensed, as upstream. Use at your own risk, and as always, read the man pages.

The original archived README follows below.

---

# NoMAD Projects Archived

Jamf has decided to archive the NoMAD repos on GitHub. Going forward they aren’t going to receive any updates. 

While they are read-only, they aren’t being deleted. That means that anyone who wants to fork and use the code is welcome to do so. Everything remains MIT licensed and open source.

The projects are still here and still open source, they just won’t be maintained by Jamf. Any existing issues or PRs have been closed.

You can see the official announcement on the [Jamf Blog](https://www.jamf.com/blog/jamf-to-archive-nomad-open-source-projects/).

There is still an active user community on the [MacAdmins Slack nomad channel](https://macadmins.slack.com/archives/C1Y2Y14QG).

As always, have fun and read the man pages.

macshome

# NoMAD 1.x

The NoMAD 1.x releases have come to a close now with NoMAD 2 closing in on release. You can find the most current release (1.3.0) of NoMAD here in the releases section.

Please take a look at the [NoMAD 2](https://github.com/jamf/NoMAD-2) repo for current and ongoing work and discussions.

Thanks for all the support!

--

***NoMAD***

Get all of AD, with none of the bind! From now on you'll have no mo' need of AD.

NoMAD allows for all of the functionality you would want from a Mac bound to
Active Directory without having to actually bind to AD.

Supports macOS 10.10 and above.

***Features***

- Get Kerberos credentials from AD to use for single sign on for all services using Windows Authentication.
- Automatically renew your Kerberos tickets based upon your desires.
- Lock screen menu item.
- Get an X509 identity from your Windows CA.
- One click access to Casper and other self-service applications if installed.
- One click access to creating a Bomgar chat session with a help desk operative, and other support options.
- Admins can push one-line CLI commands to show up as a menu item in NoMAD.
- Admins can specify LDAP servers to use instead of looking them up via SRV records.
- Sync your AD password to your local account. Including keeping the user's local keychain and FileVault passwords in sync.
- Users are warned about impending password expirations.
- Single sign on access to the users Windows home directory.
- Fully AD Site aware.
- Scripts can be triggered on network change and sign in.
- Admins can enable alternate methods of changing passwords beyond Kerberos.

Coming in future versions:

- VPN connection management for built-in VPN types.
- Getting a Kerberos ticket as a side effect of a succesful VPN connection.
- Mounting of arbitrary shares based upon configured values.
- DFS resolution without needing to be bound.
- Put x509 certificate into an 802.1x profile for use with wireless networks.

Sample screen shot:

![NoMad Screen Shot](https://gitlab.com/Mactroll/NoMAD/raw/master/screen-shot "NoMAD Screen Shot")


***Have Questions?***

Feel free to report any issues that you're having or feature requests in the Issues section of the project page.

You can find some of the team in #nomad on the Mac Admins Slack. If you're not already a member you can join [here](http://macadmins.org).

You can also discuss the development and get notified of new commits in #nomad-dev.

***Sierra Support***

NoMAD is built and primarily tested on macOS Sierra using Swift 3.

***Experimental Branch***

New features in development, or otherwise risky and irresponsible behavior goes into this branch first.

***Thanks!***

Thanks to a number of people for helping me out on this. Including those of you in the secret channel!

Also a big thanks to @owen.pragel for testing and pontificating.
