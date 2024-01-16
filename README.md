# Joypad Autoconfig Files

This repository stores joypad autoconfig files for [RetroArch](https://www.retroarch.com), the reference frontend for the libretro API.

The autoconfig files included in this repository are used to recognize input devices and automatically setup default mappings between the physical device and the [RetroPad virtual controller](https://docs.libretro.com/development/input-api/#retropad).

## How to create an autoconfig file

If your input device is not recognized by RetroArch even after updating the controller profiles, then you can generate a new profile for it from RetroArch itself.

You can find detailed instructions to do this in the [official website](https://www.retroarch.com/index.php?page=controller-autoconfig).

Please **always run `Settings` -> `Input` -> `RetroPad Binds` -> `Port 1 Controls` -> `Save Controller Profile`** in order to generate correct autoconfig file name, and file content (including `input_device`). Also, please do not manually modify our existing autoconfig files for controllers if you don't have physical access to generate autoconfig files for them by yourself.

## Uploading your own autoconfig file

If you want to share an autoconfig file that is missing in RetroArch, then you can upload it to this repository.

Please remember that the goal of sharing your autoconfig file is to create a bigger database of default input device mappings that can be used by other people.

If your mapping is custom-made for your own needs, then it will not be really useful for others.
It is better if you share more generic and reusable mappings that can act as a "default".

### To upload your autoconfig file follow these steps

#### 1. Checking for duplicates

RetroArch uses three attributes of the input device to identify which autoconfig file to use: **Vendor ID**, **Product ID** and **Device Name**.
Before uploading your file, please verify that there is no other autoconfig file matching those same three attributes already.

To verify, compare the values for `input_vendor_id`, `input_product_id` and `input_device` attributes respectively.

:warning: **Warning:** If another autoconfig file exists including the same Vendor ID, Product ID and input Device Name, then your autoconfig file will cause conflicts.

#### 2. Adding input descriptors

Input descriptors are the **labels** that RetroArch will display in the user interface (UI) to describe buttons and axes of your device.
It is recommended to add descriptors so RetroArch can display useful labels in the UI.

Input descriptor attributes are not added by default, you need to manually add the attributes inside the autoconfig file that was generated by RetroArch.
For example:

```INI
input_b_btn_label = "Cross"
input_y_btn_label = "Square"
input_a_btn_label = "Circle"
input_x_btn_label = "Triangle"
```

You will find more details about the attribute name syntax in the [Input Descriptors section](#3-input-descriptors) below.

#### 3. Testing your autoconfig file

Before uploading your autoconfig file please verify that RetroArch is correctly detecting the file and also displaying all the labels for the input device.
You can verify this in the `Settings > Input > Port 1 Controls` menu.

The best way to confirm that everything is working is:

1. Reset controller bindings to the defaults: `Settings > Input > Port 1 Controls > Reset to Default Controls`
2. Disconnect and reconnect the input device
3. Check the bindings in `Settings > Input > Port 1 Controls` to confirm that they are correct
4. If applicable, then also check the menu button binding in `Settings > Input > Hotkeys > Menu (Toggle)`

#### 4. Creating a Pull Request

To upload your autoconfig file to this repository you must create a [Pull Request](https://en.wikipedia.org/wiki/Distributed_version_control#Pull_requests).

You can learn how to create a Pull Request in Github in the [official documentation](https://help.github.com/en/articles/creating-new-files).

:warning: **Warning:** Verify that you are creating the autoconfig file in the **correct folder**.
It must be the folder with the same name used in the `input_driver` attribute in the autoconfig file.

## File Format

Autoconfig files consist of a list of attributes and their corresponding values using the following syntax:

```INI
attribute_name = value
```

All attribute names in the file use the [snake_case](https://en.wikipedia.org/wiki/Snake_case) naming scheme.

### Attribute Types

There are three types of attributes for describing an input device.

#### 1. Device Descriptors

These are attributes that identify the **physical input device** itself.
The available attributes are:

Attribute                   | Description
:---------------------------|:-------------------------------------------------
`input_driver`              | Driver in-use when the input device was detected
`input_device`              | Device Name reported by the device
`input_vendor_id`           | Vendor ID reported by the device
`input_product_id`          | Product ID reported by the device
`input_device_display_name` | Friendly display name to show in the user inteface (optional)

#### 2. Button/axes Mappings

These are attributes that describe the **mappings** between physical buttons/axes and the RetroPad virtual controller.

Button/axes attributes are named following the pattern: `input_` + `button/axis name` + `input_type`.
The `input_type` suffix can be either `_axis` for axes or `_btn` for buttons.
For example:

```INI
input_b_btn = "0"
input_y_btn = "1"
input_l_x_plus_axis = "+0"
input_l_x_minus_axis = "-0"
```

The RetroPad virtual controller layout is shown below:

![RetroPad Layout](/retropad_layout.png?raw=true)

The available attributes for input device mapping are:

Attribute               | Description
:-----------------------|:----------------------------------------------
`input_b_btn`           | Device button mapped to RetroPad's `B` button
`input_y_btn`           | Device button mapped to RetroPad's `Y` button
`input_select_btn`      | Device button mapped to RetroPad's `Select` button
`input_start_btn`       | Device button mapped to RetroPad's `Start` button
`input_up_btn`          | Device button mapped to RetroPad's `D-Pad Up` button
`input_down_btn`        | Device button mapped to RetroPad's `D-Pad Down` button
`input_left_btn`        | Device button mapped to RetroPad's `D-Pad Left` button
`input_right_btn`       | Device button mapped to RetroPad's `D-Pad Right` button
`input_a_btn`           | Device button mapped to RetroPad's `A` button
`input_x_btn`           | Device button mapped to RetroPad's `X` button
`input_l_btn`           | Device button mapped to RetroPad's `Left Shoulder` button
`input_r_btn`           | Device button mapped to RetroPad's `Right Shoulder` button
`input_l2_btn`          | Device button mapped to RetroPad's `Left Trigger` button
`input_r2_btn`          | Device button mapped to RetroPad's `Right Trigger` button
`input_l3_btn`          | Device button mapped to RetroPad's `Left Thumb` button
`input_r3_btn`          | Device button mapped to RetroPad's `Right Thumb` button
`input_l_x_plus_axis`   | Device axis mapped to RetroPad's `Left Analog` axis (right)
`input_l_x_minus_axis`  | Device axis mapped to RetroPad's `Left Analog` axis (left)
`input_l_y_plus_axis`   | Device axis mapped to RetroPad's `Left Analog` axis (down)
`input_l_y_minus_axis`  | Device axis mapped to RetroPad's `Left Analog` axis (up)
`input_r_x_plus_axis`   | Device axis mapped to RetroPad's `Right Analog` axis (right)
`input_r_x_minus_axis`  | Device axis mapped to RetroPad's `Right Analog` axis (left)
`input_r_y_plus_axis`   | Device axis mapped to RetroPad's `Right Analog` axis (down)
`input_r_y_minus_axis`  | Device axis mapped to RetroPad's `Right Analog` axis (up)
`input_menu_toggle_btn` | Device button mapped to RetroPad's `Menu` button

#### 3. Input Descriptors

These are attributes that describe the **labels** that RetroArch will display in the user interface to describe buttons and axes of the input device.
They should match the labels printed on the physical controller itself.

Input descriptor attributes are named following the pattern: `input name` + `_label`.
The `input name` part is exactly the same as defined in the [button/axes mappings section](#2-buttonaxes-mappings), including the `input_` prefix and the `_axis` or `_btn` suffix.
For example:

```INI
input_l2_btn = "5"          <-- Input mapping attribute
input_l2_btn_label = "L2"   <-- Input descriptor attribute
```

:warning: **Warning:** It is important that `input name` matches exactly the input name defined in the autoconfig file.
If the input you are describing is an axis, then the input descriptor must be for an axis as well.
For example:

```INI
input_l2_axis = "+3"         <-- Input mapping attribute

input_l2_btn_label = "L2"    <-- WRONG descriptor attribute
input_l2_axis_label = "L2"   <-- CORRECT descriptor attribute
```
