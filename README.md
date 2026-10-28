# FleetTrack Pro

FleetTrack Pro is a Windows-oriented application for managing vehicle inspections, repairs, and employee records.

## Windows installer

The repository includes a GitHub Actions workflow, **Build FleetTrack Windows EXE**, which builds an Electron/NSIS installer from `FleetTrack-v8.zip` and uploads the resulting EXE as a workflow artifact when the build succeeds.

To get the installer, open **Actions → Build FleetTrack Windows EXE**, select a successful run, and download **FleetTrack-Pro-Windows-Installer** under **Artifacts**. Extract the artifact and run the installer.

## Known issue: server does not start automatically

**Important:** After compiling and installing FleetTrack Pro, the desktop application may open without connecting to the backend server. **The server currently needs to be started manually before opening the installed application.** This is a known runtime issue; a successful EXE build does not mean automatic server startup has been fixed.

### Temporary workaround (development/source installation)

1. Keep the extracted `fleet-app` source folder available on the computer that will run the backend. Node.js and the backend dependencies are required for this workaround.
2. Open **Command Prompt** in `fleet-app\backend`.
3. Run `npm start` to launch the backend (the backend package's start script is `node src/index.js`).
4. Leave that Command Prompt window open while using FleetTrack.
5. Open the installed **FleetTrack Pro** desktop application.

If the backend fails to start, check its console output for missing environment variables, database setup, or port conflicts. The installed EXE alone may not include everything needed to run this source-based workaround on a different PC.

**Planned fix:** Package the backend and its database/Prisma resources correctly with Electron, launch the backend automatically when the desktop app starts, wait until the API is ready before loading the UI, and shut it down cleanly when the app exits.

## Build from source on Windows

Use the `BUILD-FLEETTRACK-EXE-ONE-CLICK.bat` script in the extracted `fleet-app` directory if you have the updated build kit. A successful build places the installer in `fleet-app\installer-output`. Building an installer and launching the backend are currently separate steps.

## Security and build status

Dependency audit warnings have been reported during builds. Avoid `npm audit fix --force` without testing because major upgrades may break the app. Test the installed EXE, database persistence, backend connectivity, and backup/restore before relying on it for production data.
