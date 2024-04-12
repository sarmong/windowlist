# windowlist

![screenshot](screenshot.png)

Began as a fork of my favorite Polybar script [polywins](https://github.com/uniquepointer/polywins)

Windowlist has been fully rewritten in C using the relevant parts of the source code from [wmctrl](https://github.com/Conservatory/wmctrl) and [xprop](https://gitlab.freedesktop.org/xorg/app/xprop).

## Improvements over polywins

* Fixed a bug where names would not be correct if WM_CLASS contains spaces or dots
* Option to sort the window list:
    * By horizontal position on the screen
    * By the application name

## Installation

Project directory should be in `~/.config/polybar/scripts/`

In `~/.config/polybar/scripts/windowlist/` run `make`

Add module in `~/.config/polybar/config.ini`:

```ini
[module/windowlist]
type = custom/script
exec = ~/.config/polybar/scripts/windowlist/main 2> /dev/null
tail = true
```

Add module `windowlist` in any of `modules-left`, `modules-center` or `modules-right`

## Configuration

Windowlist can be configured in `config.toml` in the root of the project.

All options are detailed here:

<table>
    <tbody>
        <tr>
            <th>Option</th>
            <th>Description</th>
            <th>Possible values</th>
        </tr>
        <tr>
            <td><code>sort_by</code></td>
            <td>Criteria to sort the list of windows</td>
            <td>
                <ul>
                    <li><code>"none"</code>: unordered (WM client list order)</li>
                    <li><code>"position"</code>: sort based on horizontal position on the screen</li>
                    <li><code>"application"</code>: sort alphabetically based on the application class</li>
                <ul>
            </td>
        </tr>
        <tr>
            <td><code>max_windows</code></td>
            <td>How many windows can be visible on the list. Number of windows that did not fit will be shown e.g. <code>(+3)</code></td>
            <td align="center">number (int)</td>
        </tr>
        <tr>
            <td><code>name</code></td>
            <td>Which X window property is considered window name (label for a window)</td>
            <td>
                <ul>
                    <li><code>"class"</code>: WM_CLASS</li>
                    <li><code>"title"</code>: WM_NAME</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td><code>name_case</code></td>
            <td>Text case for window names</td>
            <td>
                <ul>
                    <li><code>"none"</code>: don't change capitalization</li>
                    <li><code>"lowercase"</code>: all lowercase</li>
                    <li><code>"uppercase"</code>: all uppercase</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td><code>name_max_length</code></td>
            <td>Maximum length for a window name before it's truncated with <code>‥</code></td>
            <td align="center">number (int)</td>
        </tr>
        <tr>
            <td><code>name_padding</code></td>
            <td>How many spaces to add before and after a window name</td>
            <td align="center">number (int)</td>
        </tr>
        <tr>
            <td><code>empty_desktop_string</code></td>
            <td>String to show when no windows are open</td>
            <td align="center">any string</td>
        </tr>
        <tr>
            <td><code>separator_string</code></td>
            <td>String displayed between window names</td>
            <td align="center">any string</td>
        </tr>
        <tr>
            <td><code>active_window_fg_color</code></td>
            <td>Foreground color for the currently focused window</td>
            <td align="center">hex color (string)</td>
        </tr>
        <tr>
            <td><code>inactive_window_fg_color</code></td>
            <td>Foreground color for unfocused windows</td>
            <td align="center">hex color (string)</td>
        </tr>
        <tr>
            <td><code>empty_desktop_fg_color</code></td>
            <td>Foreground color for the string shown when no windows are open</td>
            <td align="center">hex color (string)</td>
        </tr>
        <tr>
            <td><code>separator_fg_color</code></td>
            <td>Foreground color for the string between window names</td>
            <td align="center">hex color (string)</td>
        </tr>
        <tr>
            <td><code>overflow_fg_color</code></td>
            <td>Foreground color for the string that indicates max windows exceeding e.g. <code>(+3)</code></td>
            <td align="center">hex color (string)</td>
        </tr>
        <tr>
            <td><code>*_bg_color</code></td>
            <td>All of the foreground colors have a background color counterpart, e.g. <code>active_window_bg_color</code></td>
            <td>
                <ul>
                    <li><code>"none"</code>: no background color</li>
                    <li>hex color (string)</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td><code>*_ul_color</code></td>
            <td>All colors also have an underline color counterpart, e.g. <code>active_window_ul_color</code><br><br>
            Note that <code>line-size</code> must be set to 1 or higher in your polybar <code>config.ini</code>, otherwise underline isn't visible.</td>
            <td>
                <ul>
                    <li><code>"none"</code>: no underline</li>
                    <li>hex color (string)</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td><code>ignored_classes</code></td>
            <td>Windows with a WM_CLASS in this array will not be shown on the bar. Strings are matched case insensitively.</td>
            <td align="center">array of strings</td>
        </tr>
        <tr>
            <td><code>window_nicknames</code></td>
            <td>A window name can be substituted with a custom name using key value pairs. The keys are matched case insensitively.</td>
            <td align="center">table of string key-value pairs</td>
        </tr>
    </tbody>
</table>

Note: polybar must be reset before changes take effect.

## Dependencies

Requires an [EWMH](https://specifications.freedesktop.org/wm-spec/wm-spec-1.3.html) compliant window manager

* Wikipedia list of EWMH compliant window managers: [link](https://en.wikipedia.org/wiki/Extended_Window_Manager_Hints#List_of_window_managers_that_support_Extended_Window_Manager_Hints)
