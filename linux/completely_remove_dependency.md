# Completely Remove a Dependency in Linux

In Linux, to remove an application and its configuration files, you can use the purge command:
```sh
sudo apt-get purge <package-name>
```

When you uninstall a package, some of its dependencies may no longer be needed by other applications on your system. These orphaned dependencies can take up disk space and slow down your system, so it's a good idea to remove them.

To remove orphaned dependencies, you can use the autoremove command:
```sh
sudo apt-get autoremove
```