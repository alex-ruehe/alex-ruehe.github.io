---
title: Run Jupyter Notebooks as a Service on macOS
author: Alex
type: posts
date: 2017-08-31T04:16:40+00:00
url: /run-jupyter-notebooks-as-a-service-on-macos/
categories:
  - Tutorial
tags:
  - data science
  - Jupyter
  - macOS
  - notebook
  - pyenv
  - Python

---
I was looking for a way to run <a href="http://jupyter.org" target="_blank" rel="noopener"><code>jupyer notebook</code></a> without using a constantly open terminal or a screen session. On macOS there is a way to create services using a .plist file and the [launchctl](http://www.launchd.info) command.

Because I use different environments for all Python related stuff, it wasn&#8217;t immediately clear to me how to do this when I&#8217;ve installed Jupyter only in a [pyenv](https://github.com/pyenv/pyenv). After some fiddling around, I finally solved it. The key was to set the working directory parameter to the directory in which the environment is loaded. In my case this is `~/notebooks` where I [automatically load the env by using a `.python-version` file](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md#pyenv-local).

Below you find the .plist file, that enables you to start/stop the notebook server using `launchctl <start|stop> local.jupyter.notebook`.

It assumes that you have a Python environenment in `/Users/USERNAME/notebooks`. So simply change it to your needs. Put the file into `/Users/USERNAME/Library/LaunchAgents` and call `launchctl load PATH_TO_FILE` once to load it. After this you can start/stop the service as described above.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Disabled</key>
    <false/>
    <key>KeepAlive</key>
    <false/>
    <key>Label</key>
    <string>local.jupyter.notebook</string>
    <key>ProgramArguments</key>
    <array>
        <string>/Users/USERNAME/.pyenv/shims/jupyter</string>
        <string>notebook</string>
        <string>--notebook-dir</string>
        <string>/Users/USERNAME/notebooks</string>
        <string>--no-browser</string>
    </array>
    <key>StandardErrorPath</key>
    <string>/Users/USERNAME/Library/LaunchAgents/jupyter-notebook.stderr</string>
    <key>StandardOutPath</key>
    <string>/Users/USERNAME/Library/LaunchAgents/jupyter-notebook.stdout</string>
    <key>WorkingDirectory</key>
    <string>/Users/USERNAME/notebooks</string>
</dict>
</plist>
```