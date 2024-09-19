# Human Interface Devices (HID) Specifications and Tools

## HID USB Device Class Definition

- The Device Class Definition for HID 1.11 is intended to supplement the USB Specification and provide HID manufacturers with the information necessary to build USB-compatible devices.

- It also specifies how the HID class drive should extract data from USB devices.

- The primary and underlying goals of the HID class definition are to:

    - be as compact as possible to save device data space

    - allow the software application to skip unknown information

    - be extensible and robust

    - support nesting and collections

    - be self-describing to allow generic software applications

## HID Usage Tables

- The HID Usage Tables 1.5 document defines constants (Usages) that can be interpreted by an application tot identify the purpose and meaning of a data field in a HID report.

- Usages are also used to define the meaning of groups of related data items.

- This is accomplished by the hierarchical assignment of Usage information to Collections.

- Usages identify the purpose of a collection and the items it contains.

- Each Input, Output, Feature, and/or Collection data item within a Collection item can be assigned a purpose with its own Usage item.

- Usages assigned to a Collection apply to the items within the collection.

- Integrated Usage Table Documents

## Tools

### Waratah

- Waratah is a HID descriptor composition tool.

- It offers a high-level of abstraction,eliminates common errors, and optimizes the descriptor to reduce byte size. It implements the HID 1.11 specification so developer don't have to.

### Nuget Packages

- Microsoft.HidTools.HidSpecification - Reference for HID specification constants, units, and public Usages

- Microsoft.HidTools.HidEngine - HID Report Descriptor Engine.
