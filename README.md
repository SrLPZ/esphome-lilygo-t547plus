# ESPHome Component for LilyGO T5 4.7" Plus (t547)

This is an external ESPHome component for the **LilyGO T5 4.7" Plus** E-Paper display (based on the ESP32-S3). 

This repository is a fork and enhancement of the original component created by [nickolay/esphome-lilygo-t547plus](https://github.com/nickolay/esphome-lilygo-t547plus).

## Key Enhancements: `scan_on()` and `scan_off()`

In E-Paper displays controlled via automated scanning/refresh interfaces, maintaining the screen active or refreshing it constantly can increase power consumption or cause unnecessary pixel burnout when the display is idle.

To solve this, this version introduces two new lambda methods to manually control when the display should refresh or poll data:
* **`- lambda: id(t5_display).scan_on();`**: Activates the display scanning/processing loop right before you trigger an update.
* **`- component.update: t5_display`**: Update display.
* **`- lambda: id(t5_display).scan_off();`**: Deactivates the scanning loop immediately after the update finishes, optimizing performance.

As shown in the example below, by setting `update_interval: never` on the display component, you gain full control and can wrap your `update` calls between `scan_on()` and `scan_off()` inside automations, button presses, or time triggers.

## Configuration Example

[basic.yaml](https://github.com/SrLPZ/esphome-lilygo-t547plus/blob/main/basic.yaml)
