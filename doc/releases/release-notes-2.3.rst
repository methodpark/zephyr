:orphan:

.. _zephyr_2.3:

Zephyr 2.3.0 (Working Draft)
############################

We are pleased to announce the release of Zephyr RTOS version 2.3.0.

Major enhancements with this release include:

* <TBD>

The following sections provide detailed lists of changes by component.

Security Vulnerability Related
******************************

The following CVEs are addressed by this release:

* CVE-2020-10022: UpdateHub Module Copies a Variable-Sized Hash String
  into a fixed-size array.
* CVE-2020-10059: UpdateHub Module Explicitly Disables TLS
  Verification
* CVE-2020-10062: Under embargo until 2020/05/25
* CVE-2020-10063: Under embargo until 2020/05/25

More detailed information can be found in:
https://docs.zephyrproject.org/latest/security/vulnerabilities.html

API Changes
***********

* HWINFO

  * The identifier data structure for hwinfo drivers is clarified.  Drivers are
    responsible for ensuring that the identifier data structure is a sequence
    of bytes. The returned ID value is not supposed to be interpreted based on
    vendor-specific assumptions of byte order and should express the identifier
    as a raw byte sequence.
    The changes have an impact on users that use the hwinfo API to identify
    their devices.
    The sam0 driver byte swaps each 32 bit word of the 128 bit identifier to
    big endian.
    The nordic driver byte swaps the entire 64 bit word to big endian.

Deprecated in this release
==========================

* Kernel

  * k_uptime_delta_32(), use k_uptime_delta()
  * Timeout values

    * All timeout values are now encapsulated k_timeout_t opaque structure when
      passing them to the kernel. If you want to revert to the previous s32_t
      type for the timeout parameter, please enable
      :option:`CONFIG_LEGACY_TIMEOUT_API`

* Bluetooth

  * BT_LE_SCAN_FILTER_DUPLICATE, use BT_LE_SCAN_OPT_FILTER_DUPLICATE instead
  * BT_LE_SCAN_FILTER_WHITELIST, use BT_LE_SCAN_OPT_FILTER_WHITELIST instead
  * bt_le_scan_param::filter_dup, use bt_le_scan_param::options instead
  * bt_conn_create_le(), use bt_conn_le_create() instead
  * bt_conn_create_auto_le(), use bt_conn_le_create_auto() instead
  * bt_conn_create_slave_le(), use bt_le_adv_start() instead with
    bt_le_adv_param::peer set to the remote peers address.
  * BT_LE_ADV_* macros, use BT_GAP_ADV_* enums instead

* Boards

  * nrf51_pca10028 has been renamed to nrf51dk_nrf51422
  * nrf51_pca10031 has been renamed to nrf51dongle_nrf51422
  * nrf52810_pca10040 has been renamed to nrf52dk_nrf52810
  * nrf52_pca10040 has been renamed to nrf52dk_nrf52832
  * nrf52833_pca10100 has been renamed to nrf52833dk_nrf52833
  * nrf52811_pca10056 has been renamed to nrf52840dk_nrf52811
  * nrf52840_pca10056 has been renamed to nrf52840dk_nrf52840
  * nrf52840_pca10059 has been renamed to nrf52840dongle_nrf52840
  * nrf9160_pca10090 has been renamed to nrf9160dk_nrf9160
  * nrf52840_pca10090 has been renamed to nrf9160dk_nrf52840
  * nrf52_pca20020 has been renamed to thingy52_nrf52832
  * nrf5340_dk_nrf5340 has been renamed to nrf5340pdk_nrf5340

* Devicetree

  * The C macros generated from devicetree. Use the new ``<devicetree.h>``
    accessor API instead; see :ref:`dt-guide` for details. Use of the legacy
    macros requires enabling :option:`CONFIG_LEGACY_DEVICETREE_MACROS`.

Removed APIs in this release
============================


Stable API changes in this release
==================================

* Bluetooth Mesh

  * The net_idx parameter has been removed from the Health Client model
    APIs since it can be derived (by the stack) from the app_idx parameter

* Networking

  * The NET_DEVICE_INIT(), NET_DEVICE_INIT_INSTANCE(), NET_DEVICE_OFFLOAD_INIT()
    and ETH_NET_DEVICE_INIT() macros changed and take a device power management
    function pointer parameter. If networking PM is not implemented for the
    specific network device, the device_pm_control_nop value can be used.

* Video

  * The video_dequeue() API call now takes a k_timeout_t for the timeout
    parameter. This reverts to s32_t if CONFIG_LEGACY_TIMEOUT_API is enabled.

* Floating Point Services

  * FLOAT and FP_SHARING Kconfig options have been renamed to FPU and FPU_SHARING,
    respectively.

Kernel
******

* <TBD>

Architectures
*************

* ARC:

  * <TBD>

* ARM:

  * <TBD>

* POSIX:

  * <TBD>

* RISC-V:

  * <TBD>

* x86:

  * <TBD>

Boards & SoC Support
********************

* Added support for these SoC series:

.. rst-class:: rst-columns

   * <TBD>

* Added support for these ARM boards:

  .. rst-class:: rst-columns

     * <TBD>

* Added support for these following shields:

  .. rst-class:: rst-columns

     * <TBD>

Drivers and Sensors
*******************

* ADC

  * <TBD>

* Bluetooth

  * <TBD>

* CAN

  * <TBD>

* Clock Control

  * <TBD>

* Console

  * <TBD>

* Counter

  * <TBD>

* Display

  * <TBD>

* DMA

  * <TBD>

* EEPROM

  * <TBD>

* Entropy

  * <TBD>

* Ethernet

  * Add SAM E54 max queue count referencing
  * Add SAM0 family support to gmac driver
  * Add sam4e support to queue in gmac
  * Add network power management support to mcux
  * Add VLAN support to enc28j60
  * Add VLAN support to stm32
  * Add Ethernet cable link status support to gmac
  * Add support for i.MXRT1060 family to mcux
  * Add support for getting manual MAC address from devicetree
  * Add support for enabling random MAC address from devicetree
  * Various fixes to setup and cache handling in gmac
  * Fix how unique MAC address is determined in mcux
  * Fix Ethernet cable link detection in gecko
  * Fix stm32 when receiving data during initialization

* Flash

  * <TBD>

* GPIO

  * <TBD>

* Hardware Info

  * <TBD>

* I2C

  * <TBD>

* I2S

  * <TBD>

* IEEE 802.15.4

  * Add Decawave DW1000 driver
  * Add "no auto start" option and local MAC address support to rf2xx
  * Add support for Frame Pending Bit (FPB) handling in nrf5
  * Add CSMA CA transmit capability to nrf5
  * Add PAN coordinator mode support to nrf5
  * Add support for promiscuous mode to nrf5
  * Add support for energy scan function to nrf5
  * Fix RX timestamp handling in nrf5
  * Various fixes to rf2xx

* Interrupt Controller

  * <TBD>

* IPM

  * <TBD>

* Keyboard Scan

  * <TBD>

* LED

  * <TBD>

* Modem

  * Add support for GSM 07.10 muxing protocol to generic GSM modem
  * Add support for modem commands that do not have a line ending
  * Add automatic detection of ublox-sara-r4 modem type
  * Add automatic setting of APN for ublox-sara-r4
  * Add sendmsg() support to ublox-sara-r4
  * Fix UDP socket closing in ublox-sara-r4
  * Fix RSSI calculation for Sara U201
  * Fix TCP context release and RX socket src/dst port assignment in wncm14a2a
  * Change PPP driver connection to generic GSM modem

* Pinmux

  * <TBD>

* PS/2

  * <TBD>

* PWM

  * <TBD>

* Sensor

  * <TBD>

* Serial

  * Add uart_mux driver that is used in GSM 07.10 muxing protocol

* SPI

  * <TBD>

* Timer

  * <TBD>

* USB

  * Add experimental USB Audio implementation.

* Video

  * <TBD>

* Watchdog

  * <TBD>

* WiFi

  * Add scan completion indication to eswifi
  * Add support to ESP8266 and ESP32


Networking
**********

* Convert networking to use new k_timeout_t infrastructure
* Enhance new TCP stack support
* Add minimal support for TFTP client (RFC 1350)
* Add support for network device driver power management
* Add support for socketpair() BSD socket API
* Add support for QEMU user networking (SLIRP)
* Add support to disable automatic network attachment in OpenThread
* Add support for Frame Pending Bit handling in OpenThread
* Add support for RX frame handling in OpenThread
* Add support for TX started notification in OpenThread
* Add support for HW CSMA CA in OpenThread
* Add support for promiscuous mode in OpenThread
* Add support for reading OPAQUE resources with OMA TLV in LWM2M
* Add config to enable PAN coordinator mode in IEEE 802.15.4
* Add config to enable promiscuous mode in IEEE 802.15.4
* Add support for subscribe in Azure cloud sample
* Add support for queue mode in lwm2m_client sample
* Add support to allow change of the QEMU Ethernet interface name
* Add support for PPP IPCP to negotiate used DNS servers
* Add support for setting hostname in DHCPv4 request
* Fix binding AF_PACKET socket type multiple times
* Fix LLDPDU data in sent LLDP packets
* Fix and enhance Google IoT sample application documentation
* Fix MQTT cloud sample when polling incoming messages
* Fix LWM2M socket error handling, and pending and reply handling during start
* Fix LWM2M retransmission logic
* Fix LWM2M Cell ID resource initialization
* Fix COAP pending and reply handling
* Fix wpan_serial sample application and enable USB during initialization
* Fix HTTP client payload issue on HTTP upload
* Fix MQTT Websocket incoming data handling and accept packets only in RX
* Fix MQTT Publish message length validation
* Fix IEEE 802.15.4 received frame length validation
* Fix IEEE 802.15.4 and avoid ACK processing when not needed
* Fix IEEE 802.15.4 and allow energy detection scan unconditionally

Bluetooth
*********

* Host:

  * <TBD>

* BLE split software Controller:

  * <TBD>

* BLE legacy software Controller:

  * <TBD>

Build and Infrastructure
************************

* <TBD>

* Devicetree

  * A new :ref:`devicetree_api` was added. This API is not generated, but is
    still included via ``<devicetree.h>``. The :ref:`dt-legacy-macros` are now
    deprecated; users should replace the generated macros with new API. The
    :ref:`dt-howtos` page has been extended for the new API, and a new
    :ref:`dt-from-c` API usage guide was also added.

Libraries / Subsystems
**********************

* Random

  * <TBD>

HALs
****

* HALs are now moved out of the main tree as external modules and reside in
  their own standalone repositories.

Documentation
*************

* <TBD>

Tests and Samples
*****************

* Added samples for USB Audio Class.

Issue Related Items
*******************

These GitHub issues were addressed since the previous 2.2.0 tagged
release:

.. comment  List derived from GitHub Issue query: ...
   * :github:`issuenumber` - issue title
