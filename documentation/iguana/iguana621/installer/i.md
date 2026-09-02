# Installer

**A Safer Installation and Upgrade Model for Iguana 6 (and Iguana X)**

Iguana is critical infrastructure software. Installing a new version should never put an existing production system at unnecessary risk.

The traditional Windows installer model was developed in an era when disk space was expensive and applications were expected to clean up after themselves. Installers commonly stopped services, removed old files, replaced binaries, migrated configuration, deleted obsolete components and restarted services.

That approach makes considerably less sense for critical infrastructure.

For Iguana, the safer model is much simpler:

> **Installing a new version of Iguana must never be capable of damaging a working Iguana installation.**

Disk space is cheap. Reliability, isolation and a straightforward rollback path are much more valuable.

## Install Each Version Independently

A new Iguana release should install into its own directory.

For example:

`C:\Program Files\iNTERFACEWARE\Iguana\<version>\`

Installing Iguana should not modify, stop, upgrade, uninstall or clean up an existing Iguana installation.

The existing Iguana continues running exactly as it did before.

The new installation initially starts as a completely fresh Iguana with its own configuration and Windows service.

This means that installing a new version is no longer an in-place upgrade. It simply creates another Iguana instance that can run alongside the existing one.

## Keep the Installer Deliberately Simple

The new Windows installer should contain as little product-specific intelligence as possible.

Its responsibilities should essentially be:

1. Create the new Iguana installation directory.
2. Copy the binaries and supporting files.
3. Establish the new Iguana instance.
4. Register an independent Windows service.
5. Create the appropriate Windows shortcuts.
6. Start or launch the new Iguana.


> **It should not modify, stop, migrate, clean up or uninstall any existing Iguana installation.**

The principle is simple:

> **The installer installs. Iguana configures.**

## Bootstrapping the Web Interface

There is one important bootstrap problem.

Iguana is administered through its web interface. Therefore, on first startup, Iguana cannot use its web interface to ask the administrator which web port the web interface should run on.

The solution is to make this automatic.

Iguana can first attempt to bind to its normal default web port, for example port 6543.

If that port is already occupied, Iguana can try the next port:

`6543 → 6544 → 6545 → ...`

until it finds an available port.

It then starts its web interface on that port and records the selected port in its local configuration.

There is no need for an installer dialog or a special native configuration interface.

Once the administrator reaches the Iguana web interface, Iguana can explain that the default port was unavailable and that another port was selected. The administrator can then change it if desired.

## The Plugin Server Port

The plugin server has a similar requirement: two concurrently running Iguana instances cannot bind to the same plugin server port.

Unlike the web port, however, the plugin server port is not required to bootstrap the administration interface.

Therefore, it can simply be configured or validated from within Iguana after the web interface has started.

This gives the two ports slightly different treatment:

**Web port:** automatically find an available port so Iguana can start.

**Plugin server port:** configure and validate it from within Iguana once the administration interface is available.

Again, this keeps Iguana-specific runtime configuration inside Iguana rather than putting it into the Windows installer.

## A Shortcut That Always Finds Iguana

A Windows shortcut such as **Iguana 6.2.1** should not contain a hard-coded URL or port number.

Instead, it can invoke Iguana itself with an option such as:

`iguana.exe --open`

Because Iguana knows the location of its own configuration, it can determine which web port that particular instance is using and open the correct local URL in the user's default browser.

Conceptually:

`Iguana shortcut → Iguana → determine configured web port → open browser`

This also means that if the administrator subsequently changes the web port, the Windows shortcut continues to work.

The installer never needs to know the port number.

## Configuration Migration Belongs Inside Iguana

Once the new Iguana is independently running, Iguana itself can provide a facility to import configuration from a previous installation.

This is much safer than having the installer perform the migration.

Iguana understands channels, ports, logs, plugins and its own configuration format. The installer should not need to understand any of those things.

Most importantly, importing configuration should **not automatically start imported channels**.

The administrator could therefore:

1. Install the new Iguana alongside the existing Iguana.
2. Start the new Iguana with a fresh configuration.
3. Open its independent web interface.
4. Configure or verify its runtime settings.
5. Import configuration from the existing Iguana.
6. Have all imported channels initially disabled - no autostart.
7. Stop one production channel on the old Iguana.
8. Start the corresponding channel on the new Iguana .
9. Verify that it behaves correctly.
10. Continue migrating channels one at a time.

The old installation remains available throughout the process.

## Resource Conflicts Are Migration Issues

Running two Iguana instances simultaneously will inevitably expose resources that cannot be shared.

An LLP listener, for example, cannot start on the new Iguana while the old Iguana still owns the same listening port.

A plugin server can have the same problem.

There may also be shared files, directories or other external resources that should not be accessed simultaneously.

These should not be problems that the installer attempts to solve automatically.

They are migration issues.

Iguana should identify conflicts where possible and present them clearly to the administrator. The administrator can then deliberately transfer ownership of each resource from the old instance to the new one.

For a listening interface, the migration may be as simple as:

`Stop old channel → Start new channel → Verify`

This makes the transition explicit rather than hiding it inside installer logic.

## Rollback Becomes Simple

The most important benefit of parallel installation is the rollback path.

Suppose an interface is migrated to a new Iguana version and something unexpected occurs.

The administrator can simply:

`Stop the channel on new Iguana → Start the channel on the old Iguana`

The old installation has not been overwritten.

Its binaries have not been replaced.

Its configuration has not been migrated in place.

Its service has not been removed.

There is nothing to reconstruct.

Rollback becomes an operational decision rather than an attempt to reverse an installation procedure.

## Uninstallation Can Also Be Simple

The same philosophy applies to uninstalling Iguana.

There is little value in writing complicated installer logic designed to determine which historical files are safe to remove.

An administrator can deliberately remove an obsolete Iguana instance once they are satisfied that it is no longer required.

There is no urgency to reclaim a relatively small amount of disk space at the expense of introducing destructive logic into an infrastructure installer.

A conservative uninstall process is preferable to an intelligent but potentially dangerous one.

## From Upgrade to Parallel Migration

The fundamental change is conceptual.

We should stop treating a new Iguana release as something that must modify an existing installation.

Instead:

> **A new Iguana release is installed independently and production is migrated to it deliberately.**

The old Iguana continues operating.

The new Iguana starts independently.

Its administration interface finds an available port automatically.

Runtime configuration is handled inside Iguana.

Existing configuration can be imported with channels disabled.

Interfaces can then be moved individually and tested before continuing.

If anything goes wrong, the old interface is still there.

This is a much better model for critical infrastructure software:

**Install independently. Configure inside Iguana. Migrate deliberately. Roll back safely.**

