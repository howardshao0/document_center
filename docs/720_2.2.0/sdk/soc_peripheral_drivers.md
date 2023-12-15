﻿# SOC Peripheral Drivers

This chapter describes the peripherals prototypes for application programming reference.

```txt
├───firmware
│   ├───platform
│   │   ├───kl720
│   │	│	├───scpu
│   │   │	│	├───drv        <--------
│   │   │	│	├───rtos
│   │   │	│	├─── ...
```

Some simple examples are provided to show how to use peripherals such as, I2C, PWM, DMA, GPIO...

```txt
├───firmware
│   ├───build
│   │   ├───example_**         <--------
│   │   ├───lib
│   │   ├───solution_xxx
```

We hope that the peripheral examples can help user to test it on your board and hopefully base it to desgign your application.   
User can also refer to kdrv usage from the middleware(mdw) folder.

```txt
├───firmware
│   ├───mdw                    <--------
│   ├─── ...
```

## Peripheral Name Description

| Name                  | Description                                           |
| --------------------- | ----------------------------------------------------- |
| kdrv_aes              | Driver - Advanced Encryption Standard                 |
| kdrv_clock            | Driver - Clock                                        |
| kdrv_crypto           | Driver - Crypto                                       |
| kdrv_gdma             | Driver - Generic  Direct Memory Access                |
| kdrv_gpio             | Driver - General Purpose Input/Output                 |
| kdrv_hash             | Driver - Hash                                         |
| kdrv_i2c              | Driver - Inter-integrated Circuit                     |
| kdrv_ipc              | Driver - Inter-Process Communication                  |
| kdrv_mpu              | Driver - Memory Protection Unit                       |
| kdrv_ncpu             | Driver - Neuro Control Process Unit                   |
| kdrv_pinmux_config    | Driver - Pin Multiplexing Configuration               |
| kdrv_pll              | Driver - Phase Locked Loop                            |
| kdrv_power            | Driver - Power                                        |
| kdrv_pwm              | Driver - Pulse Width Modulation Timer                 |
| kdrv_rtc              | Driver - Real Time Counter                            |
| kdrv_sdc              | Driver - Sd Card Host Controller                      |
| kdrv_spif_nor         | Driver - SPI Flash Controller for NOR Flash           |
| kdrv_spif_nand        | Driver - SPI Flash Controller for NAND Flash          |
| kdrv_system           | Driver - System                                       |
| kdrv_timer            | Driver - Timer/Counter                                |
| kdrv_uart             | Driver - Universal Asynchronous Receiver/Transmitter  |
| kdrv_usbd3            | Driver - USB3 Device                                  |
| kdrv_usbh2            | Driver - USB2 Host                                    |
| kdrv_wdt              | Driver - Watchdog                                     |

---

## KDRV_AES
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Data Structures
```
kdrv_aes_engine_config_t Struct Reference

Data Fields
bool 	is_config_read
bool 	is_engine_available
bool 	is_ecb_supported
bool 	is_cbc_supported
bool 	is_ctr_supported
bool 	is_cfb_supported
bool 	is_ofb_supported
bool 	is_gcm_supported
bool 	is_ccm_supported
bool 	is_xts_supported
bool 	is_cmac_supported
bool 	is_cipher_stealing_enabled
bool 	is_coutermeasure_enabled
bool 	is_key_128b_supported
bool 	is_key_192b_supported
bool 	is_key_256b_supported
uint32_t 	n_bits_counter_modes
 
Detailed Description
This structure hosts a copy of the HW configuration registers
```

### Macros
```
#define 	AES_OFFSET_CFG   0
			AES offset for Configuration word in DMA Scatter-Gather Tag.

#define 	AES_OFFSET_KEY   8
 
#define 	AES_OFFSET_IV   40
  
#define 	AES_OFFSET_KEY2   72

#define 	AES_MODEID_CBC   BIT(9)
			AES Mode Register value for CBC mode of operation.

#define 	AES_MODEID_NO_CX   0x00000000
			AES Mode Register value for AES no context.
 
#define 	AES_MODEID_AES128   0x00000000
			AES Mode Register value for AES keysize of 128 bits.

#define 	AES_MODEID_AES192   BIT(3)
			AES Mode Register value for AES keysize of 192 bits.
 
#define 	AES_MODEID_AES256   BIT(2)
			AES Mode Register value for AES keysize of 256 bits.

#define 	AES_MODEID_ENCRYPT   0x00000000
			AES Mode Register value for encryption mode.

#define 	AES_MODEID_DECRYPT   BIT(0)
			AES Mode Register value for decryption mode.
  
#define 	AES_MODEID_KEY1   BIT(6)
			AES Mode Register value to use Key1.

#define 	AES_MODEID_KEY2   BIT(7)
			AES Mode Register value to use Key2.
 
#define 	AES_HW_CFG_CBC_SUPPORTED_MASK   BIT(1)
 
#define 	AES_HW_CFG_KEY_SIZE_128_SUPPORTED_MASK   BIT(24)
 
#define 	AES_HW_CFG_KEY_SIZE_192_SUPPORTED_MASK   BIT(25)
 
#define 	AES_HW_CFG_KEY_SIZE_256_SUPPORTED_MASK   BIT(26)

#define 	AES_HW_CFG_1   (*(const volatile uint32_t*)CRYPTO_AES_HW_CFG_1_REG)
 
#define 	AES_HW_CFG_MAX_CTR_SIZE_LSB   0
 
#define 	AES_HW_CFG_MAX_CTR_SIZE_MASK   (0xFFFF<<AES_HW_CFG_MAX_CTR_SIZE_LSB)
 
#define 	AES_HW_CFG_2   (*(const volatile uint32_t*)CRYPTO_AES_HW_CFG_2_REG)

#define 	AES_IV_SIZE   16
			Size for IV in all modes except GCM.

```

### Functions
```
kdrv_status_t kdrv_aes_cbc_decrypt	(	const block_t * 	key,
										const block_t * 	iv,
										const block_t * 	ciphertext,
										block_t * 	plaintext 
									)		
kdrv_aes_cbc_decrypt decrypt operation using AES-CBC

Parameters
	[in]	key	is the key involved to decrypt the ciphertext
	[in]	iv	is the input initialization vector
	[in]	ciphertext	is the input data to decrypt
	[out]	plaintext	is the output decrypted data
Returns
	kdrv_status_t
```
```
kdrv_status_t kdrv_aes_cbc_encrypt	(	const block_t * 	key,
										const block_t * 	iv,
										const block_t * 	plaintext,
										block_t * 	ciphertext 
									)		
kdrv_aes_cbc_encrypt encryption operation using AES-CBC

Parameters
	[in]	key	is the key involved to encrypt the plaintext
	[in]	iv	is the input initialization vector
	[in]	plaintext	is the input data to encrypt
	[out]	ciphertext	is the output encrypted data
Returns
	kdrv_status_t
```
```
const struct kdrv_aes_engine_config_t * kdrv_aes_initialize	(	void 		)
	
Reads and returns the HW configuration of the AES engine.

Returns
	the HW configuration, assuming it is already read.

Warning
	kdrv_aes_initialize() must be previously called
```

## KDRV_CLOCK
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Data Structures
```
kdrv_clock_value Struct Reference

Data Fields
uint16_t 	ms
uint16_t 	ns
uint16_t 	ps
uint8_t 	div
uint8_t 	enable

Detailed Description
Structure of clock value setting.
```

### Enumerations
```
enum busmux_type

Enumerations of Bus mux division.

| Enumerator     					|
| busmux_div8	| Enum 0, 50MHz 	|
| busmux_div4   | Enum 1, 100MHz	|
| busmux_div1   | Enum 2, 400MHz	|
```
```
enum clkmux_type

Enumerations of Clock mux type.

| Enumerator     				|
| clkmux_default 	| Enum 0 	|
| clkmux_1    		| Enum 1	|
```
```
enum pll_id

Enumerations of PLL id.

| Enumerator     |
| PLL1  | Enum 0 |
| PLL2  | Enum 1 |
| PLL3  | Enum 2 |
| PLL4  | Enum 3 |
| PLL5  | Enum 4 |
| PLL6  | Enum 5 |
```
```
enum scuclkin_type

Enumerations of SCU clock in type.

| Enumerator     				|
| scuclkin_pll0div3  | Enum 0   |
| scuclkin_osc  	 | Enum 1 	|
```
### Functions
```
void kdrv_delay_us	(	uint32_t 	usec	)	

Delay us to let caller thread entering into sleep mode.

Parameters
	[in]	usec	how many us to sleep
Returns
	N/A
```
```
void kdrv_clock_axiddr_clock_set	(	T_PLLnConfig * 	pClk	)	

Set AXI DDR Clock.

Parameters
	[in]	*pClk	Pointer to pClk, see T_PLLnConfig
Returns
	N/A
```
```
void kdrv_clock_mrx1_clock_set	(	T_PLLnConfig * 	pClk	)	

Set MRX1 Clock.

Parameters
	[in]	*pClk	Pointer to pClk, see T_PLLnConfig
Returns
	N/A
```
```
void kdrv_clock_mrx0_clock_set	(	T_PLLnConfig * 	pClk	)	

Set MRX0 Clock.

Parameters
	[in]	*pClk	Pointer to pClk, see T_PLLnConfig
Returns
	N/A
```
```
void kdrv_clock_npu_clock_set	(	T_PLLnConfig * 	pClk	)	

Set NPU Clock.

Parameters
	[in]	*pClk	Pointer to pClk, see T_PLLnConfig
Returns
	N/A
```
```
void kdrv_clock_dsp_clock_set	(	T_PLLnConfig * 	pClk	)	

Set DSP Clock.

Parameters
	[in]	*pClk	Pointer to pClk, see T_PLLnConfig
Returns
	N/A
```
```
void kdrv_clock_ado_clock_set	(	T_PLLnConfig * 	pClk	)	

Set ADO Clock.

Parameters
	[in]	*pClk	Pointer to pClk, see T_PLLnConfig
Returns
	N/A
```
```
void kdrv_clock_init	(	void 		)	

Initialize all clock(AXI DDR/MRX1/MRX0/NPU/DSP/ADO)

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_clock_set_scuclkin	(	enum scuclkin_type 	type,
									bool 	enable 
								)		

Set SCU clock source in.

Parameters
	[in]	type	Pointer to pClk, see scuclkin_type
	[in]	enable	enable or disable PLL control register
Returns
	N/A
```
```
void kdrv_clock_set_bus_mux	(	enum busmux_type 	type	)	

Set bus mux.

Parameters
	[in]	type	see busmux_type
Returns
	N/A
```
```
void kdrv_clock_enable_npu_clk	(	void 		)	

Enable NPU clock.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_clock_enable_dsp_clk	(	void 		)	

Enable DSP clock.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_clock_disable_npu_clk	(	void 		)	

Disable NPU clock.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_clock_disable_dsp_clk	(	void 		)	

Disable DSP clock.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_clock_enable_u3_clk60_clk	(	void 		)	

Enable U3 clock.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_clock_disable_u3_clk60_clk	(	void 		)	

Disable U3 clock.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_clock_enable_tdc_xclk_clk	(	void 		)	

Enable TDC clock.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_clock_disable_tdc_xclk_clk	(	void 		)	

Disable TDC clock.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_clock_set_csiclk	(	uint32_t 	cam_idx,
								uint32_t 	enable 
							)		

Set CSI clock.

Parameters
	[in]	cam_idx	camera index
	[in]	enable	enable or disable camera
Returns
	N/A
```

## KDRV_CRYPTO
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Data Structures
```
kdrv_crypto_dma_regs32_t Struct Reference

Data Fields
volatile uint32_t 	fetch_addr
volatile uint32_t 	reserved_0x04
volatile uint32_t 	fetch_len
volatile uint32_t 	fetch_tag
volatile uint32_t 	push_addr
volatile uint32_t 	reserved_0x14
volatile uint32_t 	push_len
volatile uint32_t 	int_en
volatile uint32_t 	int_en_set
volatile uint32_t 	int_en_clr
volatile uint32_t 	int_stat_raw
volatile uint32_t 	int_stat
volatile uint32_t 	int_stat_clr
volatile uint32_t 	config
volatile uint32_t 	start
volatile uint32_t 	status
 
Detailed Description
Structure that represent the register map of the DMA module for 32 bus width.
```
```
kdrv_crypto_dma_descr_s Struct Reference

Data Fields
volatile void * 	addr
volatile struct kdrv_crypto_dma_descr_s * 	next_descr
volatile uint32_t 	length_irq
volatile uint32_t 	tag
 
Detailed Description
Structure that represent a descriptor for the DMA module (in scatter-gather mode).
```

### Macros
```
#define 	CRYPTO_MASTER_REG   (CRYPTO_REG_BASE + 0x00000000)
  
#define 	CRYPTO_AES_HW_CFG_1_REG   (CRYPTO_REG_BASE + 0x00000404)
 
#define 	CRYPTO_AES_HW_CFG_2_REG   (CRYPTO_REG_BASE + 0x00000408)
 
#define 	CRYPTO_HASH_HW_CFG_REG   (CRYPTO_REG_BASE + 0x0000040C)
 
#define 	WAIT_CRYPTOMASTER_WITH_REGISTER_POLLING   1
 
#define 	CRYPTOMASTER_WAITIRQ_FCT()   ;
 
#define 	TRIGGER_HARDFAULT_FCT()   ;
 
#define 	CRYPTOSOC_INCL_IPS_HW_CFG   (*((const volatile uint32_t*) CRYPTO_INCL_IPS_HW_CFG_REG))
 
#define 	CRYPTOSOC_HW_CFG_AES_IP_INCLUDED_MASK   BIT(0)
 
#define 	CRYPTOSOC_HW_CFG_HASH_IP_INCLUDED_MASK   BIT(4)
 
#define 	ALIGNED   __attribute__((aligned(0x4)))
			Align on word boundary. More...
 
#define 	BLOCK_S_CONST_ADDR   0x10000000
			value of block_s.flags to set addressing in constant mode (pointing to a FIFO) More...
 
#define 	BLOCK_S_INCR_ADDR   0x00000000
			value of block_s.flags to set addressing in increment mode (pointing to a contiguous data array) More...
 
#define 	BLOCK_S_FLAG_MASK_DMA_PROPS   0x70000000
			mask for block_s.flags to only get DMA-related options More...
 
#define 	BLK_LITARRAY(literal)   (block_t){(uint8_t *)(literal), sizeof(literal), BLOCK_S_INCR_ADDR}
  
#define 	MIN(a, b)   (a)<(b)? a:b
 
#define 	roundup_32(value)   (((value) + 3) & ~3)
 
#define 	DMA_AXI_CONFIG_FETCHER_DIRECT   0x00000000
 
#define 	DMA_AXI_CONFIG_PUSHER_DIRECT   0x00000000
 
#define 	DMA_AXI_CONFIG_FETCHER_INDIRECT   BIT(0)
 
#define 	DMA_AXI_CONFIG_PUSHER_INDIRECT   BIT(1)
 
#define 	DMA_AXI_CONFIG_STOP_FETCHER   BIT(2)
 
#define 	DMA_AXI_CONFIG_STOP_PUSHER   BIT(3)
 
#define 	DMA_AXI_CONFIG_SOFTRESET   BIT(4)
 
#define 	DMA_AXI_START_FETCH   BIT(0)
 
#define 	DMA_AXI_START_PUSH   BIT(1)
 
#define 	DMA_AXI_STATUS_MASK_PUSHER_BUSY   BIT(1)
 
#define 	DMA_AXI_STATUS_MASK_FIFOIN_NOT_EMPTY   BIT(4)
  
#define 	DMA_AXI_STATUS_MASK_SOFT_RESET   BIT(6)
 
#define 	DMA_AXI_STATUS_MASK_FIFOOUT_NDATA   0xFFFF0000
 
#define 	DMA_AXI_STATUS_FIFOOUT_NDATA_SHIFT   16
 
#define 	DMA_AXI_RAWSTAT_MASK_FETCHER_ERROR   BIT(2)
			dma_sg_regs_s.Rawstatus mask for fetcher error bit More...
 
#define 	DMA_AXI_RAWSTAT_MASK_PUSHER_ERROR   BIT(5)
			dma_sg_regs_s.Rawstatus mask for pusher error bit More...
 
#define 	DMA_AXI_INTEN_ALL_EN   0X0000003F
 
#define 	DMA_AXI_DESCR_MASK_LENGTH   0x0FFFFFFF
 
#define 	DMA_AXI_DESCR_CONST_ADDR   BIT(28)
 
#define 	DMA_AXI_DESCR_REALIGN   BIT(29)
			Indicates to the DMA to realign data on 32 bits words. More...
 
#define 	DMA_AXI_DESCR_DISCARD   BIT(30)
			Indicates to the DMA to discard fetched data. More...
   
#define 	DMA_AXI_DESCR_NEXT_STOP   ((struct kdrv_crypto_dma_descr_s*)0x00000001)
			Indicates to the DMA to not fetch another descriptor. More...
 
#define 	DMA_SG_TAG_ISCONFIG   0x00000010
			value for to direct data to parameters More...
 
#define 	DMA_SG_TAG_ISDATA   0x00000000
			value for to direct data to processing More...
 
#define 	DMA_SG_TAG_ISLAST   0x00000020
			value for specifying data as last More...
 
#define 	DMA_SG_TAG_SETCFGOFFSET(a)   ((((a)&0xFF)<<8))
			macro to set the offset in the configuration More...
 
#define 	DMA_SG_TAG_DATATYPE_HASHMSG   0x00000000
			value for specifying data type to message More...
 
#define 	DMA_SG_TAG_DATATYPE_HASHINIT   0x00000040
			value for specifying data type to initialization state More...
 
#define 	DMA_SG_TAG_DATATYPE_HASHKEY   0x00000080
			value for specifying data type to HMAC key More...
 
#define 	DMA_SG_TAG_DATATYPE_AESPAYLOAD   0x00000000
			value for specifying data type payload (will be encrypted/decrypted and authenticated) More...
 
#define 	DMA_SG_TAG_DATATYPE_AESHEADER   0x00000040
			value for specifying data type header (will only be authenticated, not encrypted/decrypted) More...

#define 	DMA_SG_TAG_PADDING_MASK   0x1F
 
#define 	DMA_SG_TAG_PADDING_OFFSET   8
 
#define 	DMA_SG_TAG_SETINVALIDBYTES(a)
			macro to set the amount of invalid bytes More...
```

### Functions
```
void kdrv_cryptodma_config_sg	(	struct kdrv_crypto_dma_descr_s * 	first_fetch_descriptor,
									struct kdrv_crypto_dma_descr_s * 	first_push_descriptor 
								)		
Configure fetch and push operations in scatter-gather mode on internal DMA.

Parameters
	[in]	first_fetch_descriptor	physical address of the first fetcher descriptor to be configured, see kdrv_crypto_dma_descr_s
	[in]	first_push_descriptor	physical address of the first pusher descriptor to be configured, see kdrv_crypto_dma_descr_s
Returns
	N/A
```
```
void kdrv_cryptodma_config_direct	(	block_t 	dest,
										block_t 	src,
										uint32_t 	length 
									)		
Configure fetch and push operations in direct mode on internal DMA.

Parameters
	[in]	src	block_t to the source data to transfer
	[in]	dest	block_t to the destination location
	[in]	length	the length in bytes to transfer (from src to dest)
Returns
	N/A
```
```
void kdrv_cryptodma_check_status	(	void 		)	

Check cryptodma status.

Parameters
	[in]	N/A	
Note
	Trigger a hardfault if any error occured
Returns
	N/A
```
```
void kdrv_cryptodma_reset	(	void 		)	

Reset the internal DMA.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_cryptodma_start	(	void 		)	
	
Start internal DMA transfer.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_cryptodma_wait	(	void 		)	

Wait until internal DMA is done.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
uint32_t kdrv_cryptodma_check_bus_error	(	void 		)	

Check cryptodma error flag.

Parameters
	[in]	N/A	
Returns
	KDRV_STATUS_CRYPTO_DMA_ERR if fifo's are not empty, KDRV_STATUS_OK otherwise
```
```
void kdrv_cryptodma_run_sg	(	struct kdrv_crypto_dma_descr_s * 	first_fetch_descriptor,
								struct kdrv_crypto_dma_descr_s * 	first_push_descriptor 
							)		
Issues an internal DMA transfer command in indirect mode.

It configures the internal DMA to issue a data transfer in indirect mode.
After that, it waits for the completion (interrupt or polling) and in case
of errors on the bus will trigger an hard fault.

Parameters
	[in]	first_fetch_descriptor	list of descriptors to fetch from
	[in]	first_push_descriptor	list of descriptors to push to
Returns
	N/A
```
```
void kdrv_map_descriptors	(	struct kdrv_crypto_dma_descr_s * 	first_fetch_descriptor,
								struct kdrv_crypto_dma_descr_s * 	first_push_descriptor,
								struct kdrv_crypto_dma_descr_s ** 	mapped_in,
								struct kdrv_crypto_dma_descr_s ** 	mapped_out 
							)		
Map software descriptors and buffers to the hardware.

Warning
	kdrv_unmap_descriptors should be called to uninitialize after transfer.
Parameters
	[in]	first_fetch_descriptor	DMA input descriptors list
	[in]	first_push_descriptor	DMA output descriptors list
	[in]	mapped_in	Pointer to the address of the mapped input descriptors list
	[in]	mapped_out	Pointer to the address of the mapped output descriptors list
Returns
	N/A
```
```
void kdrv_unmap_descriptors	(	struct kdrv_crypto_dma_descr_s * 	out_descs	)	

Unmap descriptors and buffers to the hardware.

Parameters
	[in]	out_descs	Output DMA descriptors list
Returns
	N/A
```
```
struct kdrv_crypto_dma_descr_s* kdrv_write_desc_always	(	struct kdrv_crypto_dma_descr_s * 	descr,
															volatile void * 	addr,
															const uint32_t 	length,
															const uint32_t 	flags,
															const uint32_t 	tag 
														)		
Write a descriptor and return the next updated address.

Fill the descriptor (even in case of null length) with the address to
fetch/push data, the amount of bytes to fetch/push, the additional flags
required by the DMA (like fetch in a fifo mode or discard data) and the tag
which selects the crypto engine and extra flags for this specific crypto engine.

Parameters
	[in]	descr	pointer to a descriptor to fill with others parameters
	[in]	addr	the address where data will be fetched/pushed
	[in]	length	amount of bytes to fetch/push
	[in]	flags	the extra flags describing if data are coming read like
					from a fifo (DMA_AXI_DESCR_CONST_ADDR), if it is needed
					to realign on the width of the DMA bus
					(DMA_AXI_DESCR_REALIGN) or if data can be discarded
					(DMA_AXI_DESCR_DISCARD)
	[in]	tag	contains the engine from/to fetch/push data
					(see dma_sg_EngineSelect_e), indicates
					if descriptor contains data or configuration is the last
					and specific additional information per crypto-engine.
Returns
	the address of the next descriptor available (it supposes a large
	enough array of descriptors is passed as first parameter).
```
```
void kdrv_crypto_realign_desc	(	struct kdrv_crypto_dma_descr_s * 	d	)	

Mark input descriptor as needing to be realigned by the DMA.

Parameters
	[in]	d	address of descriptor, see kdrv_crypto_dma_descr_s
Returns
	N/A
```
```
void kdrv_crypto_set_last_desc	(	struct kdrv_crypto_dma_descr_s * 	d	)	

Mark input descriptor as last of a list of descriptors.

Parameters
	[in]	d	address of last descriptor, see kdrv_crypto_dma_descr_s
Returns
	N/A
```
```
void kdrv_crypto_set_desc_invalid_bytes	(	struct kdrv_crypto_dma_descr_s * 	d,
											const uint32_t 	n_bytes 
										)		
Update the last data descriptor with the extra invalid bytes.

For the currently supported engines in software (AES, ChaCha, SHA(1-2-3)),
the corresponding HW field holds invalid bytes, meaning padding after
the last data (see the CryptoMaster Datasheet, Table 13).

This function ensures that the invalid bytes are set on a descriptor
already marked as DMA_SG_TAG_ISLAST, DMA_SG_TAG_ISDATA and also
verifies that the selected engine is currently supported before updating the descriptor.

Parameters
	[in]	d	the descriptor to update, see kdrv_crypto_dma_descr_s
	[in]	n_bytes	the extra padding to append ( < 32, 5 bits in HW).
Returns
	N/A
```

## KDRV_GDMA
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Data Structures
```
gdma_setting_t Struct Reference

Data Fields
gdma_transfer_width_t 	dst_width
gdma_transfer_width_t 	src_width
gdma_burst_size_t 	burst_size
gdma_address_control_t 	dst_addr_ctrl
gdma_address_control_t 	src_addr_ctrl
gdma_work_mode_t 	dma_mode
int 	dma_dst_req
int 	dma_src_req
 
Detailed Description
Structure of GDMA settings data setting.
```
```
gdma_cropping_descriptor_t Struct Reference

Data Fields
uint32_t 	start_dst_addr
uint32_t 	start_src_addr
uint32_t 	txfer_bytes
uint32_t 	dst_offset
uint32_t 	src_offset
uint32_t 	num_txfer
 
Detailed Description
Structure of a GDMA cropping copy descriptor.
```

### Enumerations
```
enum gdma_transfer_width_t

Enumeration of GDMA transfer size: 8/16/32 bits, this is about byte-alignment.

| Enumerator     																	|
| GDMA_TXFER_WIDTH_8_BITS 	| Enum 0, GDMA transfer size: 8 bits 					|
| GDMA_TXFER_WIDTH_16_BITS 	| Enum 1, GDMA transfer size: 16 bits 					|
| GDMA_TXFER_WIDTH_32_BITS  | Enum 2, GDMA transfer size: 32 bits, default value	|
```
```
enum gdma_burst_size_t

Enumeration of GDMA transfer burst : 1/4/8/16/32/64/128/256, this is about performance.

| Enumerator     																|
| GDMA_BURST_SIZE_1  	| Enum 0, GDMA transfer burst size: 1					|
| GDMA_BURST_SIZE_4   	| Enum 1, GDMA transfer burst size: 4					|
| GDMA_BURST_SIZE_8   	| Enum 2, GDMA transfer burst size: 8					|
| GDMA_BURST_SIZE_16   	| Enum 3, GDMA transfer burst size: 16, default value	|
| GDMA_BURST_SIZE_32   	| Enum 4, GDMA transfer burst size: 32					|
| GDMA_BURST_SIZE_64   	| Enum 5, GDMA transfer burst size: 64					|
| GDMA_BURST_SIZE_128   | Enum 6, GDMA transfer burst size: 128					|
| GDMA_BURST_SIZE_256   | Enum 7, GDMA transfer burst size: 256					|
```
```
enum gdma_address_control_t

Enumeration of DMA address control, auto-increasing/descreading or fixed.

| Enumerator     																			|
| GDMA_INCREMENT_ADDRESS   	| Enum 0, DMA address control, auto-increasing, default value	|
| GDMA_DECREMENT_ADDRESS    | Enum 1, DMA address control, auto-descreading					|
| GDMA_FIXED_ADDRESS    	| Enum 2, DMA address control, fixed							|
```
```
enum gdma_work_mode_t

Enumeration of DMA working mode, can be normal or hardware handshake mode.

| Enumerator     																	|
| GDMA_NORMAL_MODE    		| Enum 0, DMA working mode, normal mode , default value	|
| GDMA_HW_HANDSHAKE_MODE	| Enum 1, DMA working mode, hardware handshake mode		|
```
```
enum gdma_hw_request_t

DMA hardware handshake mode peripherral request definitions.

| Enumerator     																					|
| GDMA_HW_REQ_NONE     		| Enum -1, No hardware handshake mode with any peripheral controllers	|
| GDMA_HW_REQ_UART0_TX 		| Enum 0, UART0 TX (kdrv_uart)											|
| GDMA_HW_REQ_UART0_RX 		| Enum 1, UART0 RX (kdrv_uart)											|
| GDMA_HW_REQ_UART1_TX 		| Enum 2, UART1 TX (kdrv_uart)											|
| GDMA_HW_REQ_UART1_RX 		| Enum 3, UART1 RX (kdrv_uart)											|
| GDMA_HW_REQ_SPIF 			| Enum 4, SPI flash (kdrv_spif)											|
| GDMA_HW_REQ_SSP0_TX 		| Enum 5, SSP0 TX (kdrv_spi)											|
| GDMA_HW_REQ_SSP0_RX 		| Enum 6, SSP0 RX (kdrv_spi)											|
| GDMA_HW_REQ_SSP1_TX 		| Enum 7, SSP1 TX (kdrv_spi)											|
| GDMA_HW_REQ_SSP1_RX 		| Enum 8, SSP1 RX (kdrv_spi)											|
| GDMA_HW_REQ_PWM_TIMER1 	| Enum 9, PWM TIMER 1 (kdrv_pwm)										|
| GDMA_HW_REQ_PWM_TIMER2 	| Enum 10, PWM TIMER 2 (kdrv_pwm)										|
| GDMA_HW_REQ_SDC0 			| Enum 11, SDC0 (kdrv_sdc)												|
| GDMA_HW_REQ_SDC1 			| Enum 12, SDC0 (kdrv_sdc)												|
```

### Functions
```
kdrv_status_t kdrv_gdma_initialize	(	void 		)

Initialize GDMA driver and allocate necessary memory for internal use.
Initialization must be performed before any GDMA functionality.

Parameters
	[in]	N/A	
Returns
	KDRV_STATUS_OK
	KDRV_STATUS_ERROR
```
```
kdrv_status_t kdrv_gdma_uninitialize	(	void 		)	

Uninitialize GDMA driver and release allocated memory.

Parameters
	[in]	N/A	
Returns
	KDRV_STATUS_OK
```
```
kdrv_status_t kdrv_gdma_memcpy	(	uint32_t 	dst_addr,
									uint32_t 	src_addr,
									uint32_t 	num_bytes,
									gdma_xfer_callback_t 	xfer_isr_cb,
									void * 	usr_arg 
								)		
An easy-to-use function for memory-to-memory copy.
It behaves just like memcpy() (from <stdlib.h>) but it uses DMA hardware to complete the work instead of CPU resources.
If 'xfer_isr_cb' is NULL then it works as blocking mode API, otherwise as non-blocking mode API and will callback to users when it is done.
Users can directly use this functions without acquireing a GDMA handle or configuring GDMA settings.

Parameters
	[in]	dst_addr	destination address in memory
	[in]	src_addr	source address in memory
	[in]	num_bytes	number of bytes to be transfered
	[in]	xfer_isr_cb	callback function to be invoked on transfer completion.
						If it is NULL, the function is in blocking mode, otherwise non-blocking mode.
	[in]	usr_arg	user's own argument which will be feeded as an input in the callback function.
Returns
	KDRV_STATUS_OK
	KDRV_STATUS_ERROR
	KDRV_STATUS_GDMA_ERROR_NO_RESOURCE
```
```
kdrv_gdma_handle_t kdrv_gdma_acquire_handle	(	void 		)	

Acquire a GDMA handle from driver for further DMA operations.
A GDMA handle actually represents a GDMA channel.
The total number of GDMA channels depends on hardware configurations, and some are used for kdrv_gdma_memcpy(). After successfully acquiring a GDMA handle, next is to configure GDMA setting on this handle through kdrv_gdma_configure_setting()

Parameters
	[in]	N/A	
Returns
	>= 0 : Successfully acquired a GDMA handle.
	< 0 : Failed to acquire a GDMA handle.
```
```
kdrv_status_t kdrv_gdma_release_handle	(	kdrv_gdma_handle_t 	handle	)	

Release the GDMA handle which is acquired from kdrv_gdma_acquire_handle()

Parameters
	[in]	handle	Acquired GDMA handle from kdrv_gdma_acquire_handle()
Returns
	KDRV_STATUS_OK
```
```

kdrv_status_t kdrv_gdma_configure_setting	(	kdrv_gdma_handle_t 	handle,
												gdma_setting_t * 	dma_setting 
											)		
Configure GDMA settings for a given GDMA handle (channel).

There are two working mode for DMA operations : GDMA_NORMAL_MODE and GDMA_HW_HANDSHAKE_MODE.

For memory-to-memory based DMA transfer, user should configure following fields into 'dma_setting'.
@ dma_mode = GDMA_NORMAL_MODE
@ dst_width to suitable values
@ src_width to suitable values
@ burst_size to suitable values
@ dst_addr_ctrl to suitable values
@ src_addr_ctrl to suitable values

For memory-to-peripheral DMA trasfner, followings are also need to be configured properly. @ dma_mode = GDMA_HW_HANDSHAKE_MODE
@ dma_dst_req to specified value @ dma_src_req to specified value

Parameters
	[in]	handle	A handle of a GDMA channel.
	[in]	dma_setting	Specify DMA operation mode and advanced settings. see gdma_setting_t
Returns
	KDRV_STATUS_OK
```
```

kdrv_status_t kdrv_gdma_transfer	(	kdrv_gdma_handle_t 	handle,
										uint32_t 	dst_addr,
										uint32_t 	src_addr,
										uint32_t 	num_bytes,
										gdma_xfer_callback_t 	xfer_isr_cb,
										void * 	usr_arg 
									)		
Start DMA transfer with specified DMA handle, in blocking or non-blocking mode.

Before invoking this function, user must acquire a GDMA handle by kdrv_gdma_acquire_handle() and configure appropriate settings by kdrv_gdma_configure_setting().
Parameters
	[in]	handle	A handle of a GDMA channel.
	[in]	dst_addr	destination address in memory
	[in]	src_addr	source address in memory
	[in]	num_bytes	number of bytes to be transfered
	[in]	xfer_isr_cb	callback function to be invoked on transfer completion.
						If it is NULL, the function is in blocking mode, otherwise non-blocking mode.
	[in]	usr_arg	user's own argument which will be feeded as an input in the callback function.
Returns
	KDRV_STATUS_OK
	KDRV_STATUS_ERROR
```
```
kdrv_status_t kdrv_gdma_transfer	(	kdrv_gdma_handle_t 	handle,
										uint32_t 	dst_addr,
										uint32_t 	src_addr,
										uint32_t 	num_bytes,
										gdma_xfer_callback_t 	xfer_isr_cb,
										void * 	usr_arg 
									)		
Start DMA transfer with specified DMA handle, in blocking or non-blocking mode.

Before invoking this function, user must acquire a GDMA handle by kdrv_gdma_acquire_handle() and configure appropriate settings by kdrv_gdma_configure_setting().
Parameters
	[in]	handle	A handle of a GDMA channel.
	[in]	dst_addr	destination address in memory
	[in]	src_addr	source address in memory
	[in]	num_bytes	number of bytes to be transfered
	[in]	xfer_isr_cb	callback function to be invoked on transfer completion.
							If it is NULL, the function is in blocking mode, otherwise non-blocking mode.
	[in]	usr_arg	user's own argument which will be feeded as an input in the callback function.
Returns
	KDRV_STATUS_OK
	KDRV_STATUS_ERROR
```
```
kdrv_status_t kdrv_gdma_abort_transfer	(	kdrv_gdma_handle_t 	handle	)	

Abort running DMA trasnfer.

Parameters
	[in]	handle	A handle of a GDMA channel.
Returns
	KDRV_STATUS_OK
```
```
kdrv_gdma_copy_list_t kdrv_gdma_allocate_copy_list	(	kdrv_gdma_handle_t 	handle,
														uint32_t 	dst_addr[],
														uint32_t 	src_addr[],
														uint32_t 	num_bytes[],
														uint32_t 	count 
													)		
A 'copy_list' transfer represents multiple of DMA transfer on different blocks of memory from/to source and destination address.
Users can use this function to prepare a GDMA 'copy_list' data structure by information settings of memory blocks.
This function internally allocates a memory to store the 'copy_list' for users, so if it is done, remember to invoke the kdrv_gdma_free_copy_list() to free allocated memory.

Parameters
	[in]	dst_addr	An array of destination adress for a chain of DMA write destination blocks.
	[in]	src_addr	An array of source adress for a chain of DMA read destination blocks.
	[in]	num_bytes	An array of numbers to describe the number of bytes to transfer for each block.
	[in]	count	Total number of DMA chain-transfer work to be performed, i.e. array set size.
Returns
	see kdrv_gdma_copy_list_t
```
```
kdrv_status_t kdrv_gdma_free_copy_list	(	kdrv_gdma_copy_list_t 	copy_list	)	

Free the 'copy_list' which is allocated previously by kdrv_gdma_allocate_copy_list()

Parameters
	[in]	copy_list	A data struture for describing a chain of DMA transfer work.
Returns
	KDRV_STATUS_OK
```
```

kdrv_status_t kdrv_gdma_transfer_copy_list	(	kdrv_gdma_handle_t 	handle,
												kdrv_gdma_copy_list_t 	copy_list,
												gdma_xfer_callback_t 	xfer_isr_cb,
												void * 	usr_arg 
											)		
Perform a chain of DMA transfer work by a 'copy_list' in blocing or non-blocking mode.

This is the multiple-copied version of kdrv_gdma_transfer().
Before invoking this function, user must perform following calls:
@ Acquire a GDMA handle by kdrv_gdma_acquire_handle().
@ Configure appropriate settings by kdrv_gdma_configure_setting().
@ Allocate a copy_list by kdrv_gdma_allocate_copy_list().

Parameters
	[in]	handle	A handle of a GDMA channel.
	[in]	copy_list	A data struture for describing a chain of DMA transfer work.
	[in]	xfer_isr_cb	Callback function to be invoked on transfer completion.
						If it is NULL, the function is in blocking mode, otherwise non-blocking mode.
	[in]	usr_arg	user's own argument which will be feeded as an input in the callback function.
Returns
	KDRV_STATUS_OK
	KDRV_STATUS_ERROR
```
```
kdrv_status_t kdrv_gdma_memcpy_cropping	(	gdma_cropping_descriptor_t * 	cropping_desc,
											gdma_xfer_callback_t 	xfer_isr_cb,
											void * 	usr_arg 
										)		
Perform a DMA cropping-like copy by user-specified gdma_cropping_descriptor_t.

This function is like kdrv_gdma_memcpy(), and it avoid users to confgiure settings and allocate the copy_list. However the limitation is that all addresses and size and offset must be double-world (32-bit) aligned.

Parameters
	[in]	cropping_desc	Describe the source and destination cropping area and transfer bytes, see gdma_cropping_descriptor_t.
	[in]	xfer_isr_cb	Callback function to be invoked on transfer completion.
						If it is NULL, the function is in blocking mode, otherwise non-blocking mode.
	[in]	usr_arg	User's own argument which will be feeded as an input in the callback function.
Returns
	KDRV_STATUS_OK
	KDRV_STATUS_ERROR
```

## KDRV_GPIO
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Data Structures
```
gpio_attr_context Struct Reference

Data Fields
uint32_t 	gpio_pin
uint32_t 	gpio_attr
 
Detailed Description
Structure of GPIO context.
```

### Enumerations
```
enum kdrv_gpio_attribute_t

Enumerations of GPIO pin attributes, input or output, interrupt trigger settings.

| Enumerator     																							|
| GPIO_DIR_INPUT  		| 	Enum 0x1, pin direction digital input											|
| GPIO_DIR_OUTPUT 		|	Enum 0x2, pin direction digital output											|
| GPIO_INT_EDGE_RISING 	|	Enum 0x4 ,indicate pin interrupt triggered when at rising edge					|
| GPIO_INT_EDGE_FALLING |	Enum 0x8, indicate pin interrupt triggered when at falling edge					|
| GPIO_INT_EDGE_BOTH 	|	Enum 0x10, indicate pin interrupt triggered when at both edge rsising or falling|
| GPIO_INT_LEVEL_HIGH 	|	Enum 0x20, indicate pin interrupt triggered when at high voltage level			|
| GPIO_INT_LEVEL_LOW 	|	Enum 0x40, indicate pin interrupt triggered when at low voltage level			|
| GPIO_OUT_HIGH 		|	Enum 0x80, indicate pin default output level : HIGH								|
| GPIO_OUT_LOW 			|	Enum 0x100, indicate pin default output level : LOW								|
```
```
enum kdrv_gpio_pin_t

Enumerations of GPIO pin ID, there 32 GPIO pins.

| Enumerator     								|
| GPIO_PIN_0 	|	Enum 0, GPIO pin ID 0		|
| GPIO_PIN_1 	|	Enum 1, GPIO pin ID 1		|
| GPIO_PIN_2 	|	Enum 2, GPIO pin ID 2		|
| GPIO_PIN_3 	|	Enum 3, GPIO pin ID 3		|
| GPIO_PIN_4 	|	Enum 4, GPIO pin ID 4		|
| GPIO_PIN_5 	|	Enum 5, GPIO pin ID 5		|
| GPIO_PIN_6 	|	Enum 6, GPIO pin ID 6		|
| GPIO_PIN_7 	|	Enum 7, GPIO pin ID 7		|
| GPIO_PIN_8 	|	Enum 8, GPIO pin ID 8		|
| GPIO_PIN_9 	|	Enum 9, GPIO pin ID 9		|
| GPIO_PIN_10 	|	Enum 10, GPIO pin ID 10		|
| GPIO_PIN_11 	|	Enum 11, GPIO pin ID 11		|
| GPIO_PIN_12 	|	Enum 12, GPIO pin ID 12		|
| GPIO_PIN_13 	|	Enum 13, GPIO pin ID 13		|
| GPIO_PIN_14 	|	Enum 14, GPIO pin ID 14		|
| GPIO_PIN_15 	|	Enum 15, GPIO pin ID 15		|
| GPIO_PIN_16 	|	Enum 16, GPIO pin ID 16		|
| GPIO_PIN_17 	|	Enum 17, GPIO pin ID 17		|
| GPIO_PIN_18 	|	Enum 18, GPIO pin ID 18		|
| GPIO_PIN_19 	|	Enum 19, GPIO pin ID 19		|
| GPIO_PIN_20 	|	Enum 20, GPIO pin ID 20		|
| GPIO_PIN_21 	|	Enum 21, GPIO pin ID 21		|
| GPIO_PIN_22 	|	Enum 22, GPIO pin ID 22		|
| GPIO_PIN_23 	|	Enum 23, GPIO pin ID 23		|
| GPIO_PIN_24 	|	Enum 24, GPIO pin ID 24		|
| GPIO_PIN_25 	|	Enum 25, GPIO pin ID 25		|
| GPIO_PIN_26 	|	Enum 26, GPIO pin ID 26		|
| GPIO_PIN_27 	|	Enum 27, GPIO pin ID 27		|
| GPIO_PIN_28 	|	Enum 28, GPIO pin ID 28		|
| GPIO_PIN_29 	|	Enum 29, GPIO pin ID 29		|
| GPIO_PIN_30 	|	Enum 30, GPIO pin ID 30		|
| GPIO_PIN_31 	|	Enum 31, GPIO pin ID 31		|
```

### Functions
```
kdrv_status_t kdrv_gpio_initialize	(	void 		)	

GPIO driver initialization, this must be invoked once before any GPIO manipulations.

Parameters
	[in]	N/A	
Returns
	KDRV_STATUS_OK only
```
```
kdrv_status_t kdrv_gpio_uninitialize	(	void 		)	

GPIO driver uninitialization.
This function disables the corresponding clock and frees resources allocated for GPIO operations.

Parameters
	[in]	N/A	
Returns
	KDRV_STATUS_OK only
```
```
kdrv_status_t kdrv_gpio_set_attribute	(	kdrv_gpio_pin_t 	pin,
											uint32_t 	attributes 
										)		
set pin attributes for a specified GPIO pin
it must be well set up before GPIO pin to be used.

Parameters
	[in]	pin	After configuring the desired pin as a GPIO pin, the corresponding GPIO pin name should be used as kdp_gpio_pin_e indicated
	[in]	attributes	This is to specify the function of specified GPIO pin,
						for digital output, set only DIR_OUTPUT,
						for digital input for read, set only DIR_INPUT,
						for interrupt usage, set DIR_INPUT and one of EDGE or LEVEL trigger attributes, this implies pin is used as an interrupt input
Returns
	KDRV_STATUS_OK only
```
```
kdrv_status_t kdrv_gpio_register_callback	(	gpio_interrupt_callback_t 	gpio_isr_cb,
												void * 	usr_arg 
											)		
register user callback with user argument for GPIO interrupt in this callback can get interrupts for all GPIO pins

Parameters
	[in]	gpio_isr_cb	user callback function for GPIO interrupts, see gpio_interrupt_callback_t
	[in]	usr_arg	Pointer to user's argument
Returns
	KDRV_STATUS_OK only
```
```
kdrv_status_t kdrv_gpio_set_interrupt	(	kdrv_gpio_pin_t 	pin,
											bool 	isEnable 
										)		
set interrupt enable/disable for a specified GPIO pin

Parameters
	[in]	pin	GPIO pin ID, see kdrv_gpio_pin_t
	[in]	isEnable	enable/disable
Returns
	KDRV_STATUS_OK only
```
```

kdrv_status_t kdrv_gpio_set_debounce	(	kdrv_gpio_pin_t 	pin,
											bool 	isEnable,
											uint32_t 	debounce_clock 
										)		
set debounce enable/disable with clock setting in Hz

This can enable internal debouncing hardware for interrupt mode to eliminate the switch bounce.
It is very useful for connecting devices like a switch button or a keypad thing.

Parameters
	[in]	pin	GPIO pin ID, see kdrv_gpio_pin_t
	[in]	isEnable	enable/disable
	[in]	debounce_clock	The debouncing clock frequency in Hz
Returns
	KDRV_STATUS_OK only
```
```
kdrv_status_t kdrv_gpio_write_pin	(	kdrv_gpio_pin_t 	pin,
										bool 	value 
									)		
write GPIO digitial pin value

This function writes a high or low value to a digital pin.
The specified pin must be configured as digital output.

Parameters
	[in]	pin	GPIO pin ID, see kdrv_gpio_pin_t
	[in]	value	Output value as digital high or digital low
Returns
	KDRV_STATUS_OK only
```
```

kdrv_status_t kdrv_gpio_read_pin	(	kdrv_gpio_pin_t 	pin,
										bool * 	pValue 
									)		
read GPIO digitial pin value

This function read a high or low value from a digital pin.
The specified pin must be configured as digital input and not in interrupt mode.

Parameters
	[in]	pin	GPIO pin ID, see kdrv_gpio_pin_t
	[out]	pValue	Pointer to a value to read out GPIO voltage level
Returns
	KDRV_STATUS_OK only
```

## KDRV_HASH
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Data Structures
```
hash_regs_s Struct Reference

Data Fields
volatile uint32_t 	config
 
Detailed Description
Structure of hash config information.
```
```
kdrv_hash_engine_config_t Struct Reference

Data Fields
bool 	is_config_read
bool 	is_engine_available
bool 	is_md5_enabled
bool 	is_sha1_enabled
bool 	is_sha224_enabled
bool 	is_sha256_enabled
bool 	is_sha384_enabled
bool 	is_sha512_enabled
bool 	is_hmac_enabled
bool 	is_sm3_enabled
bool 	is_padding_enabled
 
Detailed Description
Structures hosts a copy of the HW configuration registers
```

### Macros
```
#define 	HASH_CONF_MODE_SHA256   BIT(3)
 
#define 	HASH_CONF_HMAC   0x00000100
 
#define 	HASH_CONF_HWPAD   0x00000200
 
#define 	HASH_CONF_FINAL   0x00000400
  
#define 	HASH_HW_CFG_SHA256_SUPPORTED_MASK   BIT(3)
 
#define 	HASH_HW_CFG_PADDING_SUPPORTED_MASK   BIT(16)
 
#define 	HASH_HW_CFG_HMAC_SUPPORTED_MASK   BIT(17)
  
#define 	HASH_HW_CFG   (*(const volatile uint32_t*)CRYPTO_HASH_HW_CFG_REG)
 
#define 	SHA256_BLOCKSIZE   64
			Size of SHA256 data block in bytes. More...
 
#define 	SHA256_INITSIZE   32
			Size of SHA256 initialization value in bytes. More...
 
#define 	SHA256_DIGESTSIZE   32
			Size of SHA256 digest in bytes. More...
 
#define 	SX_HASH_ARRAY_MAX_ENTRIES   8
			Maximum number of entries in kdrv_hash_array_blk and kdrv_hash_hmac_array_blk. More...
```

### Functions
```
const struct kdrv_hash_engine_config_t* kdrv_hash_initialize	(	void 		)

Reads and returns the HW configuration of the hash engine.

Parameters
	[in]	N/A	
Returns
	kdrv_hash_engine_config_t*, Pointer to const kdrv_hash_engine_config_t
```
```
const struct kdrv_hash_engine_config_t* kdrv_hash_engine_get_config	(	void 		)	

Simply returns the HW configuration, which should have been previously read using kdrv_hash_initialize().

Warning
	kdrv_hash_initialize() must be previously called
Parameters
	[in]	N/A	
Returns
	kdrv_hash_engine_config_t*, Pointer to const r kdrv_hash_engine_config_t
```
```
uint32_t kdrv_hash_get_digest_size	(	kdrv_hash_fct_t 	hash_fct	)	

Get digest size in bytes for the given hash_fct.

Parameters
	[in]	hash_fct	hash function. See kdrv_hash_fct_t.
Returns
	digest size in bytes, or 0 if invalid hash_fct
```
```
uint32_t kdrv_hash_get_block_size	(	kdrv_hash_fct_t 	hash_fct	)	

Get block size in bytes for the given hash_fct.

Parameters
	[in]	hash_fct	hash function. see kdrv_hash_fct_t.
Returns
	block size in bytes, or 0 if invalid hash_fct
```
```
uint32_t kdrv_hash_get_state_size	(	kdrv_hash_fct_t 	hash_fct	)	

Get state size in bytes for the given hash_fct.

Parameters
	[in]	hash_fct	hash function. see kdrv_hash_fct_t.
Returns
	state size in bytes, or 0 if invalid hash_fct
```
```
kdrv_status_t kdrv_hash_array_blk	(	kdrv_hash_fct_t 	hash_fct,
										block_t 	data_in[],
										const unsigned int 	entries,
										block_t 	data_out 
									)		
Compute hash digest of the content of data_in and write the result in data_out.

Parameters
	[in]	hash_fct	hash function to use. Seekdrv_hash_fct_t.
	[in]	data_in	array of input data to process, see block_t
	[in]	entries	length of array data_in
	[out]	data_out	output digest, see block_t
Returns
	see kdrv_status_t
```
```
kdrv_status_t kdrv_hash_blk	(	kdrv_hash_fct_t 	hash_fct,
								block_t 	data_in,
								block_t 	data_out 
							)		
Compute hash digest of the content of data_in and write the result in data_out.

Parameters
	[in]	hash_fct	hash function to use, see kdrv_hash_fct_t.
	[in]	data_in	input data to process, see block_t
	[out]	data_out	output digest, see block_t
Returns
	KDRV_STATUS_OK if execution was successful, see kdrv_status_t
```

## KDRV_I2C
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Data Structures
```
i2c_attr_context Struct Reference

Data Fields
uint32_t 	i2c_port
uint32_t 	i2c_speed
uint32_t 	i2c_devaddr
 
Detailed Description
Structure of I2C device instances.
```

### Enumerations
```
enum kdrv_i2c_bus_speed_t

Enumerations of I2C bus speed.

| Enumerator     																|
| KDRV_I2C_SPEED_100K 	| Enum 0, Kdrv I2C bus speed 100KHz, standard mode		|
| KDRV_I2C_SPEED_200K 	| Enum 1, Kdrv I2C bus speed 200KHz						|
| KDRV_I2C_SPEED_400K 	| Enum 2, Kdrv I2C bus speed 400KHz, fast mode			|
| KDRV_I2C_SPEED_1M 	| Enum 3, Kdrv I2C bus speed 1MHz, fast plus mode		|
```
```
enum kdrv_i2c_ctrl_t

Enumerations of I2C controller instances.

| Enumerator     												|
| KDRV_I2C_CTRL_0 		| Enum 0, Kdrv I2C controller 0			|
| KDRV_I2C_CTRL_1 		| Enum 1, Kdrv I2C controller 1			|
| KDRV_I2C_CTRL_2 		| Enum 2, Kdrv I2C controller 2			|
| TOTAL_KDRV_I2C_CTRL 	| Enum 3, Total Kdrv I2C controllers	|
```

### Functions
```
kdrv_status_t kdrv_i2c_initialize	(	void 		)	

Initializes Kdrv I2C driver (as master) and configures it for the specified speed.

Returns
	kdrv_status_t see kdrv_status_t
Note
	This API MUST be called before using the Read/write APIs for I2C.
```
```
kdrv_status_t kdrv_i2c_uninitialize	(	kdrv_i2c_ctrl_t 	ctrl_id	)	

Uninitializes Kdrv I2C driver.

Parameters
	[in]	ctrl_id	see kdrv_i2c_ctrl_t
Returns
	kdrv_status_t see kdrv_status_t
```
```

kdrv_status_t kdp_i2c_transmit	(	kdrv_i2c_ctrl_t 	ctrl_id,
									uint16_t 	slave_addr,
									uint8_t * 	data,
									uint32_t 	num,
									bool 	with_STOP 
								)		
transmit data to a specified slave address, the STOP condition can be optionally not generated.
This function will first set START condition then send slave address for write operations;
if 9th bit is NACK, it returns DEV_NACK error, and if it is ACK,
controller will continue to send out all data with specified number of bytes,
once it is done it will set STOP condition while the 'with_STOP' is KDP_BOOL_TRUE.
For every byte transmission, it returns DEV_NACK error while encountering NACK at 9th bit.

Parameters
	[in]	ctrl_id	see kdrv_i2c_ctrl_t
	[in]	slave_addr	Address of the slave(7-bit by default)
	[in]	data	data buffer address
	[in]	num	Length of data to be written (in bytes)
	[in]	with_STOP	STOP condition will be generated or not
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdp_i2c_receive	(	kdrv_i2c_ctrl_t 	ctrl_id,
									uint16_t 	slave_addr,
									uint8_t * 	data,
									uint32_t 	num,
									bool 	with_STOP 
								)		
receive data from a specified slave address, the STOP condition can be optionally not generated.

This function will first set START condition then send slave address for write operations;
if 9th bit is NACK, it returns DEV_NACK error, and if it is ACK,
controller will continue to send out all data with specified number of bytes,
once it is done it will set STOP condition while the 'with_STOP' is KDP_BOOL_TRUE.
For every byte transmission, it returns DEV_NACK error while encountering NACK at 9th bit

Parameters
	[in]	ctrl_id	see kdrv_i2c_ctrl_t
	[in]	slave_addr	Address of the slave(7-bit by default)
	[out]	data	data buffer address
	[in]	num	Length of data to be written (in bytes)
	[in]	with_STOP	STOP condition will be generated or not
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_i2c_write_register	(	kdrv_i2c_ctrl_t 	ctrl_id,
											uint16_t 	slave_addr,
											uint16_t 	reg,
											uint16_t 	reg_size,
											uint16_t 	len,
											uint8_t * 	data 
										)		
specialized function to write to the register of slave device, register address can be 1 or 2 bytes.

Parameters
	[in]	ctrl_id	see kdrv_i2c_ctrl_t
	[in]	slave_addr	Address of the slave(7-bit by default)
	[in]	reg	Register address
	[in]	reg_size	Length of register address
	[in]	len	Length of data to be written (in bytes).
	[in]	data	data write register value
Returns
	kdrv_status_t see kdrv_status_t
```
```

kdrv_status_t kdrv_i2c_read_register	(	kdrv_i2c_ctrl_t 	ctrl_id,
											uint16_t 	slave_addr,
											uint16_t 	reg,
											uint16_t 	reg_size,
											uint16_t 	len,
											uint8_t * 	data 
										)		
specialized function to read from the register of slave device, register address can be 1 or 2 bytes.

Parameters
	[in]	ctrl_id	see kdrv_i2c_ctrl_t
	[in]	slave_addr	Address of the slave(7-bit by default)
	[in]	reg	Register address
	[in]	reg_size	Length of register address
	[in]	len	Length of data to be read (in bytes).
	[out]	data	data buffer to read register value
Returns
	kdrv_status_t see kdrv_status_t
```

## KDRV_IPC
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Functions
```
void kdrv_ipc_enable_to_ncpu_int	(	void 		)	

Enable SCPU IPC interrupt to NCPU.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_ipc_trigger_to_ncpu_int	(	void 		)	

Trigger SCPU IPC interrup[t to NCPU.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_ipc_clear_from_ncpu_int	(	void 		)	

Clear SCPU IPC interrupt to NCPU.

Parameters
	[in]	N/A	
Returns
	N/A
```

## KDRV_MPU
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Functions
```
void kdrv_mpu_config	(	void 		)	

config memorty protect space, siram + niram

Returns
	N/A
```
```
void kdrv_mpu_niram_enable	(	void 		)	

mpu protect enable for niram memory space

Returns
	N/A
```
```
void kdrv_mpu_niram_disable	(	void 		)	

mpu protect disable for niram memory space

Returns
	N/A
```

## KDRV_NCPU
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Functions
```
void kdrv_ncpu_set_stall	(	uint8_t 	is_stall	)	

ncpu_set_stall() set ncpu into stall mode

Parameters
	[in]	is_stall	0: none, 1: stall
Returns
	N/A
```
```
void kdrv_ncpu_boot_initialize	(	void 		)	

ncpu boot initialize

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_ncpu_reset	(	void 		)	

ncpu reset

Parameters
	[in]	N/A	
Returns
	N/A
```
```
uint8_t kdrv_get_stall_status	(	void 		)	

Get stall status.

Parameters
	[in]	N/A	
Returns
	N/A
```

## KDRV_PINMUX_CONFIG
Please refer to ./firmware/utils/pinmux/Kneron_pinmux_gpio_config_720.xlsm for the detailed pin multiplexer information

Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Enumerations
```
enum kdrv_pin_name

Enumerations of KDP520 all configurable pins.

| Enumerator     								|
| KDRV_PIN_X_SPI_CS_N 		| Enum 0			|
| KDRV_PIN_X_SPI_CLK 		| Enum 1			|
| KDRV_PIN_X_SPI_DO 		| Enum 2			|
| KDRV_PIN_X_SPI_DI 		| Enum 3			|
| KDRV_PIN_X_SPI_WP_N 		| Enum 4			|
| KDRV_PIN_X_SPI_HOLD_N 	| Enum 5			|
| KDRV_PIN_X_I2C0_CLK 		| Enum 6			|
| KDRV_PIN_X_I2C0_DATA 		| Enum 7			|
| KDRV_PIN_X_I2C1_CLK 		| Enum 8			|
| KDRV_PIN_X_I2C1_DATA 		| Enum 9			|
| KDRV_PIN_X_I2C2_CLK 		| Enum 10			|
| KDRV_PIN_X_I2C2_DATA 		| Enum 11			|
| KDRV_PIN_X_SSP0_CLK 		| Enum 12			|
| KDRV_PIN_X_SSP0_CS0 		| Enum 13			|
| KDRV_PIN_X_SSP0_CS1 		| Enum 14			|
| KDRV_PIN_X_SSP0_DI 		| Enum 15			|
| KDRV_PIN_X_SSP0_DO 		| Enum 16			|
| KDRV_PIN_X_SSP1_CLK 		| Enum 17			|
| KDRV_PIN_X_SSP1_CS 		| Enum 18			|
| KDRV_PIN_X_SSP1_DI 		| Enum 19			|
| KDRV_PIN_X_SSP1_DO 		| Enum 20			|
| KDRV_PIN_X_SSP1_DCX 		| Enum 21			|
| KDRV_PIN_X_JTAG_TRSTN 	| Enum 22			|
| KDRV_PIN_X_JTAG_TDI 		| Enum 23			|
| KDRV_PIN_X_JTAG_TMS 		| Enum 24			|
| KDRV_PIN_X_JTAG_TCK 		| Enum 25			|
| KDRV_PIN_X_DSP_TRSTN 		| Enum 26			|
| KDRV_PIN_X_DSP_TDI 		| Enum 27			|
| KDRV_PIN_X_DSP_TDO 		| Enum 28			|
| KDRV_PIN_X_DSP_TMS 		| Enum 29			|
| KDRV_PIN_X_DSP_TCK 		| Enum 30			|
| KDRV_PIN_X_UART0_TX 		| Enum 31			|
| KDRV_PIN_X_UART0_RX 		| Enum 32			|
| KDRV_PIN_X_TRACE_CLK 		| Enum 33			|
| KDRV_PIN_X_TRACE_DATA0 	| Enum 34			|
| KDRV_PIN_X_TRACE_DATA1 	| Enum 35			|
| KDRV_PIN_X_TRACE_DATA2 	| Enum 36			|
| KDRV_PIN_X_TRACE_DATA3 	| Enum 37			|
| KDRV_PIN_X_UART1_RI 		| Enum 38			|
| KDRV_PIN_X_SD1_D3 		| Enum 39			|
| KDRV_PIN_X_SD1_D2 		| Enum 40			|
| KDRV_PIN_X_SD1_D1 		| Enum 41			|
| KDRV_PIN_X_SD1_D0 		| Enum 42			|
| KDRV_PIN_X_SD1_CMD 		| Enum 43			|
| KDRV_PIN_X_SD1_CLK 		| Enum 44			|
| KDRV_PIN_X_SD0_D3 		| Enum 45			|
| KDRV_PIN_X_SD0_D2 		| Enum 46			|
| KDRV_PIN_X_SD0_D1 		| Enum 47			|
| KDRV_PIN_X_SD0_D0 		| Enum 48			|
| KDRV_PIN_X_SD0_CMD 		| Enum 49			|
| KDRV_PIN_X_SD0_CLK 		| Enum 50			|
| KDRV_PIN_X_SD0_CARD_PWN 	| Enum 51			|
| KDRV_PIN_X_SD0_CARD_DET 	| Enum 52			|
| KDRV_PIN_X_JTAG_TDO 		| Enum 53			|
| KDRV_PIN_X_PWM0 			| Enum 54			|
| KDRV_PIN_X_PWM1 			| Enum 55			|
| KDRV_PIN_X_DPI_PCLKI 		| Enum 56			|
| KDRV_PIN_X_DPI_VSI 		| Enum 57			|
| KDRV_PIN_X_DPI_HSI 		| Enum 58			|
| KDRV_PIN_X_DPI_DEI 		| Enum 59			|
| KDRV_PIN_X_DPI_DATAI0 	| Enum 60			|
| KDRV_PIN_X_DPI_DATAI1 	| Enum 61			|
| KDRV_PIN_X_DPI_DATAI2 	| Enum 62			|
| KDRV_PIN_X_DPI_DATAI3 	| Enum 63			|
| KDRV_PIN_X_DPI_DATAI4 	| Enum 64			|
| KDRV_PIN_X_DPI_DATAI5 	| Enum 65			|
| KDRV_PIN_X_DPI_DATAI6 	| Enum 66			|
| KDRV_PIN_X_DPI_DATAI7 	| Enum 67			|
| KDRV_PIN_X_DPI_DATAI8 	| Enum 68			|
| KDRV_PIN_X_DPI_DATAI9 	| Enum 69			|
| KDRV_PIN_X_DPI_DATAI10 	| Enum 70			|
| KDRV_PIN_X_DPI_DATAI11 	| Enum 71			|
| KDRV_PIN_X_DPI_DATAI12 	| Enum 72			|
| KDRV_PIN_X_DPI_DATAI13 	| Enum 73			|
| KDRV_PIN_X_DPI_DATAI14 	| Enum 74			|
| KDRV_PIN_X_DPI_DATAI15 	| Enum 75			|
| KDRV_PIN_X_DPI_PCLKO 		| Enum 76			|
| KDRV_PIN_X_DPI_VSO 		| Enum 77			|
| KDRV_PIN_X_DPI_HSO 		| Enum 78			|
| KDRV_PIN_X_DPI_DEO 		| Enum 79			|
| KDRV_PIN_X_DPI_DATAO0 	| Enum 80			|
| KDRV_PIN_X_DPI_DATAO1 	| Enum 81			|
| KDRV_PIN_X_DPI_DATAO2 	| Enum 82			|
| KDRV_PIN_X_DPI_DATAO3 	| Enum 83			|
| KDRV_PIN_X_DPI_DATAO4 	| Enum 84			|
| KDRV_PIN_X_DPI_DATAO5 	| Enum 85			|
| KDRV_PIN_X_DPI_DATAO6 	| Enum 86			|
| KDRV_PIN_X_DPI_DATAO7 	| Enum 87			|
| KDRV_PIN_X_DPI_DATAO8 	| Enum 88			|
| KDRV_PIN_X_DPI_DATAO9 	| Enum 89			|
| KDRV_PIN_X_DPI_DATAO10 	| Enum 90			|
| KDRV_PIN_X_DPI_DATAO11 	| Enum 91			|
```
```
enum kdrv_pinmux_mode

Enumerations of KDP520 pinmux modes.

| Enumerator     											|
| PIN_MODE_0 	| Enum 0, Pimux mode 0						|
| PIN_MODE_1 	| Enum 1, Pimux mode 1						|
| PIN_MODE_2 	| Enum 2, Pimux mode 2						|
| PIN_MODE_3 	| Enum 3, Pimux mode 3, for GPIO mode only	|
| PIN_MODE_4 	| Enum 4, Pimux mode 4						|
| PIN_MODE_5 	| Enum 5, Pimux mode 5						|
| PIN_MODE_6 	| Enum 6, Pimux mode 6						|
| PIN_MODE_7 	| Enum 7, Pimux mode 7						|
```
```
enum kdrv_pin_pull

Enumerations of KDP520 pull status.

| Enumerator     									|
| PIN_PULL_NONE 	| Enum 0, Pin none				| 
| PIN_PULL_UP 		| Enum 1, Pin pull up			| 
| PIN_PULL_DOWN 	| Enum 2, Pin pull down			| 
```
```
enum kdrv_pin_driving

Enumerations of KDP520 output driving capability.

| Enumerator     							| 
| PIN_DRIVING_4MA 	| Enum 0, 4mA			| 
| PIN_DRIVING_8MA 	| Enum 1, 8mA			|
| PIN_DRIVING_12MA 	| Enum 2, 12mA			| 
| PIN_DRIVING_16MA 	| Enum 3, 16mA			|
```

### Functions
```
void kdrv_pinmux_initialize	(	void 		)	

Pinmux init.

Returns
	N/A
```
```
void kdrv_pinmux_config	(	kdrv_pin_name 	pin,
							kdrv_pinmux_mode 	mode,
							kdrv_pin_pull 	pull_type,
							kdrv_pin_driving 	driving 
						)		
Pinmux configure.

Parameters
	[in]	pin	see kdrv_pin_name
	[in]	mode	see kdrv_pinmux_mode
	[in]	pull_type	see kdrv_pin_pull
	[in]	driving	see kdrv_pin_driving
Returns
	N/A
```

## KDRV_PLL
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Data Structures
```
T_PLL0Config Struct Reference

Data Fields
uint32_t 	dwHz
uint32_t 	dwPLL0Setting
void(* 	pDelayFunc )(uint32_t)
 
Detailed Description
Structure of PLL0 config information.
```
```
T_PLLnConfig Struct Reference

Data Fields
uint32_t 	dwHz
uint32_t 	dwPLLnSetting
uint32_t 	dwPLLnLockTime
uint32_t 	dwMux
uint32_t 	dwDivider
 
Detailed Description
Structure of PLLn config information.
```

### Macros
```
#define 	XTAL_MHZ   12
 
#define 	SCPU_MHZ   400
 
#define 	AXI_DDR_MHZ   533
 
#define 	MRX1_MHZ   720
 
#define 	MRX0_MHZ   720
 
#define 	NPU_MHZ   700
 
#define 	DSP_MHZ   500
 
#define 	AUDIO_MHZ   12p288
 
#define 	PLL_AXI_DDR   1
 
#define 	PLL_MRX1   2
 
#define 	PLL_MRX0   3
 
#define 	PLL_NPU   4
 
#define 	PLL_DSP   5
 
#define 	PLL_ADO   6
 
#define 	PLL0_1200_MS   1
 
#define 	PLL0_1200_NS   100
 
#define 	PLL0_1200_PS   0
 
#define 	PLL0_1200_IS   0
 
#define 	PLL0_1200_MS_MASK   (PLL0_1200_MS<<16)
 
#define 	PLL0_1200_NS_MASK   (((PLL0_1200_NS&0xFF)<<24)&((PLL0_1200_NS&0x100)<<19))
 
#define 	PLL0_1200_PS_MASK   (PLL0_1200_PS<< 8)
 
#define 	PLL0_1200_IS_MASK   (PLL0_1200_IS<<20)
 
#define 	SCPU_CLKIN_MUX_12MHZ   1
 
#define 	SCPU_CLKIN_MUX_12MHZ_MASK   (SCPU_CLKIN_MUX_12MHZ<<4)
 
#define 	SCPU_CLKIN_MUX_PLL0_DIV3   0
 
#define 	SCPU_CLKIN_MUX_PLL0_DIV3_MASK   (SCPU_CLKIN_MUX_PLL0_DIV3<<4)
 
#define 	PLL0_STABLE   1
 
#define 	PLL0_NOT_STABLE   0
 
#define 	PLL1_400_MS   3
 
#define 	PLL1_400_NS   100
 
#define 	PLL1_400_PS   0
 
#define 	PLL1_400_IS   0
 
#define 	PLL1_400_MS_MASK   ((PLL1_400_MS&0x07 )<<16)
 
#define 	PLL1_400_NS_MASK   ((PLL1_400_NS&0x1FF)<<20)
 
#define 	PLL1_400_PS_MASK   ((PLL1_400_PS&0x0F )<<12)
 
#define 	PLL1_400_IS_MASK   ((PLL1_400_IS&0x03 )<< 8)
 
#define 	PLL1_TIMER   0x4C0
 
#define 	PLL1_TIMER   0x4C0
 
#define 	PLL1_TIMER   0x4C0
 
#define 	PLL1_TIMER   0x4C0
 
#define 	PLL1_TIMER   0x4C0
 
#define 	PLL1_668_MS   3
 
#define 	PLL1_668_NS   167
 
#define 	PLL1_668_PS   0
 
#define 	PLL1_668_IS   0
 
#define 	PLL1_668_MS_MASK   ((PLL1_668_MS&0x07 )<<16)
 
#define 	PLL1_668_NS_MASK   ((PLL1_668_NS&0x1FF)<<20)
 
#define 	PLL1_668_PS_MASK   ((PLL1_668_PS&0x0F )<<12)
 
#define 	PLL1_668_IS_MASK   ((PLL1_668_IS&0x03 )<< 8)
 
#define 	PLL1_800_MS   3
 
#define 	PLL1_800_NS   200
 
#define 	PLL1_800_PS   0
 
#define 	PLL1_800_IS   0
 
#define 	PLL1_800_MS_MASK   ((PLL1_800_MS&0x07 )<<16)
 
#define 	PLL1_800_NS_MASK   ((PLL1_800_NS&0x1FF)<<20)
 
#define 	PLL1_800_PS_MASK   ((PLL1_800_PS&0x0F )<<12)
 
#define 	PLL1_800_IS_MASK   ((PLL1_800_IS&0x03 )<< 8)
 
#define 	PLL1_933_MS   3
 
#define 	PLL1_933_NS   233
 
#define 	PLL1_933_PS   0
 
#define 	PLL1_933_IS   0
 
#define 	PLL1_933_MS_MASK   ((PLL1_933_MS&0x07 )<<16)
 
#define 	PLL1_933_NS_MASK   ((PLL1_933_NS&0x1FF)<<20)
 
#define 	PLL1_933_PS_MASK   ((PLL1_933_PS&0x0F )<<12)
 
#define 	PLL1_933_IS_MASK   ((PLL1_933_IS&0x03 )<< 8)
 
#define 	PLL1_1066_MS   3
 
#define 	PLL1_1066_NS   266
 
#define 	PLL1_1066_PS   0
 
#define 	PLL1_1066_IS   0
 
#define 	PLL1_1066_MS_MASK   ((PLL1_1066_MS&0x07 )<<16)
 
#define 	PLL1_1066_NS_MASK   ((PLL1_1066_NS&0x1FF)<<20)
 
#define 	PLL1_1066_PS_MASK   ((PLL1_1066_PS&0x0F )<<12)
 
#define 	PLL1_1066_IS_MASK   ((PLL1_1066_IS&0x03 )<< 8)
 
#define 	PLL2_1440_MS   1
 
#define 	PLL2_1440_NS   120
 
#define 	PLL2_1440_PS   0
 
#define 	PLL2_1440_IS   0
 
#define 	PLL2_1440_MS_MASK   ((PLL2_1440_MS&0x07 )<<16)
 
#define 	PLL2_1440_NS_MASK   ((PLL2_1440_NS&0x1FF)<<20)
 
#define 	PLL2_1440_PS_MASK   ((PLL2_1440_PS&0x0F )<<12)
 
#define 	PLL2_1440_IS_MASK   ((PLL2_1440_IS&0x03 )<< 8)
 
#define 	PLL2_TIMER   0x4C0
 
#define 	PLL3_1440_MS   1
 
#define 	PLL3_1440_NS   120
 
#define 	PLL3_1440_PS   0
 
#define 	PLL3_1440_IS   0
 
#define 	PLL3_1440_MS_MASK   ((PLL3_1440_MS&0x07 )<<16)
 
#define 	PLL3_1440_NS_MASK   ((PLL3_1440_NS&0x1FF)<<20)
 
#define 	PLL3_1440_PS_MASK   ((PLL3_1440_PS&0x0F )<<12)
 
#define 	PLL3_1440_IS_MASK   ((PLL3_1440_IS&0x03 )<< 8)
 
#define 	PLL3_TIMER   0x4C0
 
#define 	PLL4_800_MS   2
 
#define 	PLL4_800_NS   133
 
#define 	PLL4_800_PS   0
 
#define 	PLL4_800_IS   0
 
#define 	PLL4_800_MS_MASK   ((PLL4_800_MS&0x07 )<<16)
 
#define 	PLL4_800_NS_MASK   ((PLL4_800_NS&0x1FF)<<20)
 
#define 	PLL4_800_PS_MASK   ((PLL4_800_PS&0x0F )<<12)
 
#define 	PLL4_800_IS_MASK   ((PLL4_800_IS&0x03 )<< 8)
 
#define 	PLL4_TIMER   0x4C0
 
#define 	PLL4_TIMER   0x4C0
 
#define 	PLL4_TIMER   0x4C0
 
#define 	PLL4_TIMER   0x4C0
 
#define 	PLL4_1000_MS   2
 
#define 	PLL4_1000_NS   167
 
#define 	PLL4_1000_PS   0
 
#define 	PLL4_1000_IS   0
 
#define 	PLL4_1000_MS_MASK   ((PLL4_1000_MS&0x07 )<<16)
 
#define 	PLL4_1000_NS_MASK   ((PLL4_1000_NS&0x1FF)<<20)
 
#define 	PLL4_1000_PS_MASK   ((PLL4_1000_PS&0x0F )<<12)
 
#define 	PLL4_1000_IS_MASK   ((PLL4_1000_IS&0x03 )<< 8)
 
#define 	PLL4_1200_MS   2
 
#define 	PLL4_1200_NS   200
 
#define 	PLL4_1200_PS   0
 
#define 	PLL4_1200_IS   0
 
#define 	PLL4_1200_MS_MASK   ((PLL4_1200_MS&0x07 )<<16)
 
#define 	PLL4_1200_NS_MASK   ((PLL4_1200_NS&0x1FF)<<20)
 
#define 	PLL4_1200_PS_MASK   ((PLL4_1200_PS&0x0F )<<12)
 
#define 	PLL4_1200_IS_MASK   ((PLL4_1200_IS&0x03 )<< 8)
 
#define 	PLL4_1400_MS   1
 
#define 	PLL4_1400_NS   116
 
#define 	PLL4_1400_PS   0
 
#define 	PLL4_1400_IS   0
 
#define 	PLL4_1400_MS_MASK   ((PLL4_1400_MS&0x07 )<<16)
 
#define 	PLL4_1400_NS_MASK   ((PLL4_1400_NS&0x1FF)<<20)
 
#define 	PLL4_1400_PS_MASK   ((PLL4_1400_PS&0x0F )<<12)
 
#define 	PLL4_1400_IS_MASK   ((PLL4_1400_IS&0x03 )<< 8)
 
#define 	PLL5_800_MS   2
 
#define 	PLL5_800_NS   133
 
#define 	PLL5_800_PS   0
 
#define 	PLL5_800_IS   0
 
#define 	PLL5_800_MS_MASK   ((PLL5_800_MS&0x07 )<<16)
 
#define 	PLL5_800_NS_MASK   ((PLL5_800_NS&0x1FF)<<20)
 
#define 	PLL5_800_PS_MASK   ((PLL5_800_PS&0x0F )<<12)
 
#define 	PLL5_800_IS_MASK   ((PLL5_800_IS&0x03 )<< 8)
 
#define 	PLL5_TIMER   0x4C0
 
#define 	PLL5_TIMER   0x4C0
 
#define 	PLL5_TIMER   0x4C0
 
#define 	PLL5_TIMER   0x4C0
 
#define 	PLL5_TIMER   0x4C0
 
#define 	PLL5_900_MS   2
 
#define 	PLL5_900_NS   150
 
#define 	PLL5_900_PS   0
 
#define 	PLL5_900_IS   0
 
#define 	PLL5_900_MS_MASK   ((PLL5_900_MS&0x07 )<<16)
 
#define 	PLL5_900_NS_MASK   ((PLL5_900_NS&0x1FF)<<20)
 
#define 	PLL5_900_PS_MASK   ((PLL5_900_PS&0x0F )<<12)
 
#define 	PLL5_900_IS_MASK   ((PLL5_900_IS&0x03 )<< 8)
 
#define 	PLL5_1000_MS   2
 
#define 	PLL5_1000_NS   167
 
#define 	PLL5_1000_PS   0
 
#define 	PLL5_1000_IS   0
 
#define 	PLL5_1000_MS_MASK   ((PLL5_1000_MS&0x07 )<<16)
 
#define 	PLL5_1000_NS_MASK   ((PLL5_1000_NS&0x1FF)<<20)
 
#define 	PLL5_1000_PS_MASK   ((PLL5_1000_PS&0x0F )<<12)
 
#define 	PLL5_1000_IS_MASK   ((PLL5_1000_IS&0x03 )<< 8)
 
#define 	PLL5_1200_MS   2
 
#define 	PLL5_1200_NS   200
 
#define 	PLL5_1200_PS   0
 
#define 	PLL5_1200_IS   0
 
#define 	PLL5_1200_MS_MASK   ((PLL5_1200_MS&0x07 )<<16)
 
#define 	PLL5_1200_NS_MASK   ((PLL5_1200_NS&0x1FF)<<20)
 
#define 	PLL5_1200_PS_MASK   ((PLL5_1200_PS&0x0F )<<12)
 
#define 	PLL5_1200_IS_MASK   ((PLL5_1200_IS&0x03 )<< 8)
 
#define 	PLL5_1500_MS   2
 
#define 	PLL5_1500_NS   250
 
#define 	PLL5_1500_PS   0
 
#define 	PLL5_1500_IS   0
 
#define 	PLL5_1500_MS_MASK   ((PLL5_1500_MS&0x07 )<<16)
 
#define 	PLL5_1500_NS_MASK   ((PLL5_1500_NS&0x1FF)<<20)
 
#define 	PLL5_1500_PS_MASK   ((PLL5_1500_PS&0x0F )<<12)
 
#define 	PLL5_1500_IS_MASK   ((PLL5_1500_IS&0x03 )<< 8)
 
#define 	PLL6_1536_MS   2
 
#define 	PLL6_1536_NS   192
 
#define 	PLL6_1536_PS   0
 
#define 	PLL6_1536_IS   0
 
#define 	PLL6_1536_MS_MASK   ((PLL6_1536_MS&0x07 )<<16)
 
#define 	PLL6_1536_NS_MASK   ((PLL6_1536_NS&0x1FF)<<20)
 
#define 	PLL6_1536_PS_MASK   ((PLL6_1536_PS&0x0F )<<12)
 
#define 	PLL6_1536_IS_MASK   ((PLL6_1536_IS&0x03 )<< 8)
 
#define 	PLL6_TIMER   0x4C0
 
#define 	PLLn_LOCKED   1
 
#define 	PLLn_ENABLE   1
 
#define 	PLLn_ENABLE_MASK   (PLLn_ENABLE<<0)
 
#define 	PLLn_DISABLE   0
 
#define 	PLLn_DISABLE_MASK   (PLLn_DISABLE<<0)
```

### Enumerations
```
enum scpu_clk_setting

Enumerations of list supported SCPU clock.

| Enumerator     								|
| SCPU_400_CFG1 			| Enum 0			|
| SCPU_CLK_TOTAL_SUPPORTED 	| Enum 1			|
```
```
enum axi_ddr_clk_setting

Enumerations of list supported AXI/DDR clock.

| Enumerator     									|
| AXI_DDR_200_CFG1 				| Enum 0			| 
| AXI_DDR_333_CFG1 				| Enum 1			| 
| AXI_DDR_400_CFG1 				| Enum 2			| 
| AXI_DDR_466_CFG1 				| Enum 3			| 
| AXI_DDR_533_CFG1 				| Enum 4			| 
| AXI_DDR_CLK_TOTAL_SUPPORTED 	| Enum 5			| 
```
```
enum mrx1_clk_setting

Enumerations of list supported MRX1 clock

| Enumerator     									|
| MRX1_720_CFG1  				| Enum 0			|
| MRX1_CLK_TOTAL_SUPPORTED   	| Enum 1			|
```
```
enum mrx0_clk_setting

Enumerations of list supported MRX0 clock.

| Enumerator     									|
| MRX0_720_CFG1 			| Enum 0				| 
| MRX0_CLK_TOTAL_SUPPORTED 	| Enum 1				| 
```
```
enum npu_clk_setting

Enumerations of list supported NPU clock.

| Enumerator     									|
| NPU_200_CFG1 				| Enum 0				|
| NPU_300_CFG1 				| Enum 1				|
| NPU_300_CFG2 				| Enum 2				|
| NPU_350_CFG1 				| Enum 3				|
| NPU_400_CFG1 				| Enum 4				|
| NPU_500_CFG1 				| Enum 5				|
| NPU_600_CFG1 				| Enum 6				|
| NPU_600_CFG2 				| Enum 7				|
| NPU_700_CFG1 				| Enum 8				|
| NPU_CLK_TOTAL_SUPPORTED 	| Enum 9				|
```
```
enum dsp_clk_setting

Enumerations of list supported DSP clock.

| Enumerator     									|
| DSP_200_CFG1 				| Enum 0				|
| DSP_200_CFG2 				| Enum 1				|
| DSP_300_CFG1 				| Enum 2				|
| DSP_400_CFG1 				| Enum 3				|
| DSP_400_CFG2 				| Enum 4				|
| DSP_500_CFG1 				| Enum 5				|
| DSP_CLK_TOTAL_SUPPORTED 	| Enum 6				|
```
```
enum audio_clk_setting

Enumerations of list supported Audio clock.

| Enumerator     									|
| ADO_12p288_CFG1 			| Enum 0				|
| ADO_CLK_TOTAL_SUPPORTED 	| Enum 1				|
```

## KDRV_POWER
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Enumerations
```
enum kdrv_power_domain_t

Enumerations of kl720 power domains.

| Enumerator     																	|
| POWER_DOMAIN_BAS 	| Enum 1, Power to BAS power domain triggered by wake-up events	|
| POWER_DOMAIN_NOM 	| Enum 2, Power to NOR power domain controlled by software		|
| POWER_DOMAIN_MRX 	| Enum 3, Power to MRX power domain controlled by software		|
| POWER_DOMAIN_UHO 	| Enum 4, Power to UHO power domain controlled by software		|
| POWER_DOMAIN_NPU 	| Enum 5, Power to NPU power domain controlled by software		|
| POWER_DOMAIN_UDR 	| Enum 6, Power to UDR power domain controlled by software		|
```
```
enum kdrv_power_ops_t

Enumerations of kl720 power operations.

| Enumerator     										|
| POWER_OPS_FCS 				| Enum 0				|
| POWER_OPS_CHANGE_BUS_SPEED 	| Enum 1				|
```
```
enum kdrv_power_mode_t

Enumerations of kl720 power modes.

| Enumerator     									|
| POWER_MODE_FULLOFF 		| Enum 0				|
| POWER_MODE_AUX_PWR_ON 	| Enum 1				|
| POWER_MODE_BASE 			| Enum 2				|
| POWER_MODE_NOR 			| Enum 3				|
| POWER_MODE_IMG_DETECT 	| Enum 4				|
| POWER_MODE_UVC 			| Enum 5				|
| POWER_MODE_AI_TEST 		| Enum 6				|
| POWER_MODE_USB_DEVICE 	| Enum 7				|
| POWER_MODE_AI_RUNING 		| Enum 8				|
| POWER_MODE_USB_AI 		| Enum 9				|
| POWER_MODE_UVC_AI 		| Enum 10				|
| POWER_MODE_UVC_AI_PASS 	| Enum 11				|
| POWER_MODE_ALL_AXI_ON 	| Enum 12				|
| POWER_MODE_DORM_USB_S 	| Enum 13				|
| POWER_MODE_SNOZ_USB_S 	| Enum 14				|
| POWER_MODE_DORM 			| Enum 15				|
| POWER_MODE_SNOZ 			| Enum 16				|
| POWER_MODE_MAX 			| Enum 17				|
```

### Functions
```
void kdrv_power_sw_reset	(	void 		)

Watchdog reset.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
kdrv_status_t kdrv_power_ops	(	kdrv_power_ops_t 	ops	)	

Power operation.

Parameters
	[in]	ops	see kdrv_power_ops_t
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_power_set_domain	(	uint32_t 	domain	)	

Set power domain.
There are three powe domain in Kneron kl720 chip, see kdrv_power_domain_t

Parameters
	[in]	domain	see kdrv_power_domain_t
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_power_set_powermode	(	kdrv_power_mode_t 	next_pm	)	

Set power mode.

Parameters
	[in]	next_pm	see kdrv_power_mode_t
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_power_softoff	(	kdrv_power_mode_t 	pm	)	

Shutdown the power supply to all blocks, except the logic in the RTC domain and DDR memory is in self-refresh state.

Parameters
	[in]	mode	see kdrv_power_mode_t
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_power_sleep	(	void 		)	

Set power mode into sleep.

Returns
	kdrv_status_t see kdrv_status_t
```

## KDRV_PWM
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Macros
```
#define 	APB_CLK   APB_CLOCK
```

### Enumerations
```
enum pwm_id

Enumerations of all timer callback event return status.

| Enumerator     											|
| PWM_ID_1 		| Enum 1, PWM timer callback instance 1		|
| PWM_ID_2 		| Enum 2, PWM timer callback instance 2		|
```
```
enum pwmpolarity

Enumerations of polarity of a PWM signal.

| Enumerator     																																		|
| PWM_POLARITY_NORMAL 		| Enum 0, A high signal for the duration of the duty-cycle, followed by a low signal for the remainder of the pulse period	|
| PWM_POLARITY_INVERSED 	| Enum 1, A low signal for the duration of the duty-cycle, followed by a high signal for the remainder of the pulse period	|
```

### Functions
```
kdrv_status_t kdrv_pwm_config	(	pwm_id 	pwmid,
									pwmpolarity 	polarity,
									uint32_t 	duty,
									uint32_t 	period,
									bool 	ns2clkcnt 
								)		
kdrv_pwm_config
After config pwm timer via this API, you should call kdrv_pwm_enable() to let pwm timer work well.

Parameters
	[in]	timer	pwm timer id, see pwm_id
	[in]	polarity	polarity, see pwmpolarity
	[in]	duty_ms	duty cycle(ms)
	[in]	period_ms	period(ms)
Returns
	kdrv_status_t see kdrv_status_t
Note
	Example:
	kdrv_pwm_config(PWM_ID_1, PWM_POLARITY_NORMAL, duty, PWM0_FREQ_CNT, 0);
	kdrv_pwm_enable(PWM_ID_1);
```
```
kdrv_status_t kdrv_pwm_enable	(	pwm_id 	pwmid	)	

kdrv_pwm_enable

Parameters
	[in]	timer	pwm timer id, see pwm_id
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_pwm_disable	(	pwm_id 	pwmid	)	

kdrv_pwm_disable

Parameters
	[in]	timer	pwm timer id, see pwm_id
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_pwm_initialize	(	void 		)	

kdrv_pwm_initialize

Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_pwm_uninitialize	(	void 		)	

kdrv_pwm_uninitialize

Returns
	kdrv_status_t see kdrv_status_t
```

## KDRV_RTC
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Data Structures
```
rtc_time_s Struct Reference

Data Fields
uint32_t 	sec: 8
uint32_t 	min: 8
uint32_t 	hour: 8
uint32_t 	weekday: 8

Detailed Description
Structure of RTC time setting.
```
```
rtc_date_s Struct Reference

Data Fields
uint32_t 	date: 8
uint32_t 	month: 8
uint32_t 	year: 8
uint32_t 	century: 8
 
Detailed Description
Structure of RTC date setting.
```

### Macros
```
#define 	SECS_PER_MIN   60
 
#define 	MINS_PER_HOUR   60
 
#define 	HOURS_PER_DAY   24
 
#define 	SECS_PER_HOUR   (MINS_PER_HOUR * SECS_PER_MIN)
 
#define 	SECS_PER_DAY   (HOURS_PER_DAY * SECS_PER_HOUR)
 
#define 	MAX_DAYS_PER_MONTH   31
 
#define 	MONTH_PER_YEAR   12
 
#define 	YEARS_PER_CENTURY   100
 
#define 	CENTURY_PER_100   100
 
#define 	DAYS_PER_WEEK   7
 
#define 	DAYS_PER_YEAR   365
```

### Enumerations
```
enum alarm_type

Enumerations of all alarm typefor kdrv_timer_set.

| Enumerator     								|
| ALARM_IN_SECS 		| Enum 1				|
| ALARM_IN_DATE_TIME 	| Enum 2				|
```
```
enum periodic_interrupt

Enumerations of periodic interrupt setting.

| Enumerator     																|
| PERIODIC_MONTH_INT 	| Enum 0, Periodic interrupt output signal each month	|
| PERIODIC_DAY_INT 		| Enum 1, Periodic interrupt output signal each day		|
| PERIODIC_HOUR_INT 	| Enum 2, Periodic interrupt output signal each hour	|
| PERIODIC_MIN_INT 		| Enum 3, Periodic interrupt output signal each minute	|
| PERIODIC_SEC_INT 		| Enum 4, Periodic interrupt output signal each second	|
```

### Functions
```
void kdrv_rtc_set_attribute	(	rtc_time_s * 	time,
								rtc_date_s * 	date 
							)		
Set RTC attribute - date and time.

Parameters
	[in]	*time	Pointer to time, see rtc_time_s
	[in]	*date	Pointer to date, see rtc_date_s
Note
	If date is NULL, RTC driver would use default date value(01/06/2020)
	If time is NULL, RTC driver would use default time value(07:11:00 Mon(1))
Returns
	N/A
```
```

void kdrv_rtc_get_date_time	(	rtc_date_s * 	date,
								rtc_time_s * 	time 
							)		
Get current date and time configuration on RTC driver.

Parameters
	[in]	*time	Pointer to time, see rtc_time_s
	[in]	*date	Pointer to date, see rtc_date_s
Returns
	N/A
```
```
void kdrv_rtc_get_date_time_in_secs	(	uint32_t * 	date_time_in_secs	)	

Get current date and time configuration in seconds.

Parameters
	[in]	*date_time_in_secs	Pointer to date and time in seconds
Returns
	N/A
```
```
void kdrv_rtc_periodic_enable	(	periodic_interrupt 	per_int_type	)	

Enable an period RTC interrupt.

Parameters
	[in]	per_int_type	see periodic_interrupt
Returns
	N/A
```
```
void kdrv_rtc_sec_enable	(	void 		)	

Enable an event in each second.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_rtc_sec_disable	(	void 		)	

Disable an event in each second.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_rtc_alarm_enable	(	alarm_type 	alm_type,
								void * 	param1,
								void * 	param2 
							)		
Enable RTC alarm.

Parameters
	[in]	alm_type	see alarm_type
	[in]	*param1	Pointer to the first input parameter
	[in]	*param2	Pointer to the first input parameter
Note
	If alm_type is ALARM_IN_SECS, param1 standards for time in seconds
	If alm_type is ALARM_IN_DATE_TIME, param1 standards for rtc_date_s, and param2 standards for rtc_time_s
Returns
	N/A
```
```
void kdrv_rtc_alarm_disable	(	void 		)	

Disable RTC alarm.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_rtc_initialize	(	void 		)

Initialize RTC with default value, date: 01/06/2020 and time: 07:11:00 Mon(1)

Parameters
	[in]	N/A	
Returns
	N/A
```

## KDRV_SDC
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Data Structures
```
struct  	kdrv_sdc_reg_t
 
struct  	kdrv_sdc_flow_info_t
 
struct  	kdrv_sd_status_t
 
struct  	kdrv_sdc_csd_v1_t
 
struct  	kdrv_sdc_csd_v2_t
 
struct  	kdrv_sdc_sd_scr_t
 
struct  	kdrv_sdc_sdcard_info_t
 
struct  	kdrv_sdc_sd_host_t
 
struct  	kdrv_sdc_adma2desc_table_t
 
struct  	kdrv_sdc_res_t
 
struct  	kdrv_sdc_mmc_csd_t
 
struct  	kdrv_sdc_mmc_ext_csd_t
```

### Macros
```
#define 	ADMA2_NUM_OF_LINES   64
 
#define 	CARD_TYPE_UNKNOWN   0
 
#define 	MEMORY_CARD_TYPE_SD   1
 
#define 	MEMORY_CARD_TYPE_MMC   2
 
#define 	SDIO_TYPE_CARD   3
 
#define 	MEMORY_SDIO_COMBO   4
 
#define 	SCR_LENGTH   8
 
#define 	SD_STATUS_LENGTH   64
 
#define 	EXT_CSD_LENGTH   512
 
#define 	SDHCI_SCR_SUPPORT_4BIT_BUS   0x4
 
#define 	SDHCI_SCR_SUPPORT_1BIT_BUS   0x1
 
#define 	WAIT_CMD_COMPLETE   BIT(0)
 
#define 	WAIT_TRANS_COMPLETE   BIT(1)
 
#define 	WAIT_DMA_INTR   BIT(2)
 
#define 	WAIT_BLOCK_GAP   BIT(3)
 
#define 	KDRV_SDC_BASE   SDIO_REG_BASE
 
#define 	SDHCI_TXMODE_DMA_EN   BIT(0)
 
#define 	SDHCI_TXMODE_BLKCNT_EN   BIT(1)
 
#define 	SDHCI_TXMODE_AUTOCMD12_EN   BIT(2)
 
#define 	SDHCI_TXMODE_AUTOCMD23_EN   (2 << 2)
 
#define 	SDHCI_TXMODE_READ_DIRECTION   BIT(4)
 
#define 	SDHCI_TXMODE_WRITE_DIRECTION   (0 << 4)
 
#define 	SDHCI_TXMODE_MULTI_SEL   BIT(5)
 
#define 	SDHCI_CMD_IDX_SHIFT   0x08
 
#define 	SDHCI_CMD_TYPE_SHIFT   0x06
 
#define 	SDHCI_CMD_DATA_PRESEL_SHIFT   0x05
 
#define 	SDHCI_CMD_NO_RESPONSE   0x00
 
#define 	SDHCI_CMD_RTYPE_R2   0x09
 
#define 	SDHCI_CMD_RTYPE_R3R4   0x02
 
#define 	SDHCI_CMD_RTYPE_R1R5R6R7   0x1A
 
#define 	SDHCI_CMD_RTYPE_R1BR5B   0x1B
 
#define 	SDHCI_CMD_TYPE_NORMAL   0x00
 
#define 	SDHCI_CMD_TYPE_SUSPEND   0x01
 
#define 	SDHCI_CMD_TYPE_RESUME   0x02
 
#define 	SDHCI_CMD_TYPE_ABORT   0x03
 
#define 	SDHCI_CMD_DATA_PRESENT   0x01
 
#define 	SDHCI_REG_DATA_PORT   0x20
 
#define 	SDHCI_REG_PRE_STATE   0x24
 
#define 	SDHCI_STS_CMD_INHIBIT   BIT(0)
 
#define 	SDHCI_STS_CMD_DAT_INHIBIT   BIT(1)
 
#define 	SDHCI_STS_DAT_LINE_ACT   BIT(2)
 
#define 	SDHCI_STS_WRITE_TRAN_ACT   BIT(8)
 
#define 	SDHCI_STS_READ_TRAN_ACT   BIT(9)
 
#define 	SDHCI_STS_BUFF_WRITE   BIT(10)
 
#define 	SDHCI_STS_BUFF_READ   BIT(11)
 
#define 	SDHCI_STS_CARD_INSERT   BIT(16)
 
#define 	SDHCI_STS_CARD_STABLE   BIT(17)
 
#define 	SDHCI_STS_CARD_WP   BIT(19)
 
#define 	SDHCI_STS_DAT_LINE_LEVEL   (0xF << 20)
 
#define 	SDHCI_STS_CMD_LINE_LEVEL   BIT(24)
 
#define 	SDHCI_REG_HC   0x28
 
#define 	SDHCI_HC_LED_ON   BIT(0)
 
#define 	SDHCI_HC_BUS_WIDTH_4BIT   BIT(1)
 
#define 	SDHCI_HC_HI_SPEED   BIT(2)
 
#define 	SDHCI_HC_USE_ADMA2   BIT(3)
 
#define 	SDHCI_HC_BUS_WIDTH_8BIT   BIT(5)
 
#define 	SDHCI_HC_CARD_DETECT_TEST   BIT(6)
 
#define 	SDHCI_HC_CARD_DETECT_SIGNAL   BIT(7)
 
#define 	SDHCI_POWER_ON   BIT(0)
 
#define 	SDHCI_POWER_180   (5 << 1)
 
#define 	SDHCI_POWER_300   (6 << 1)
 
#define 	SDHCI_POWER_330   (7 << 1)
 
#define 	SDHCI_STOP_AT_BLOCK_GAP_REQ   BIT(0)
 
#define 	SDHCI_CONTINUE_REQ   BIT(1)
 
#define 	SDHCI_READ_WAIT_CTL   BIT(2)
 
#define 	SDHCI_INT_AT_BLOCK_GAP   BIT(3)
 
#define 	SDHCI_REG_CLK_CTRL   0x2C
 
#define 	SDHCI_CLK_CTRL_LOW_CLK_SEL_SHIFT   8
 
#define 	SDHCI_CLK_CTRL_UP_CLK_SEL_SHIFT   6
 
#define 	SDHCI_CLK_CTRL_INTERNALCLK_EN   BIT(0)
 
#define 	SDHCI_CLK_CTRL_INTERNALCLK_STABLE   BIT(1)
 
#define 	SDHCI_CLK_CTRL_SDCLK_EN   BIT(2)
 
#define 	SDHCI_CLK_CTRL_CLK_GEN_SEL_PRO   BIT(5)
 
#define 	SDHCI_SOFTRST_ALL   BIT(0)
 
#define 	SDHCI_SOFTRST_CMD   BIT(1)
 
#define 	SDHCI_SOFTRST_DAT   BIT(2)
 
#define 	SDHCI_REG_INTR_STATE   0x30
 
#define 	SDHCI_INTR_STS_ERR   BIT(15)
 
#define 	SDHCI_INTR_STS_CARD_INTR   BIT(8)
 
#define 	SDHCI_INTR_STS_CARD_REMOVE   BIT(7)
 
#define 	SDHCI_INTR_STS_CARD_INSERT   BIT(6)
 
#define 	SDHCI_INTR_STS_BUFF_READ_READY   BIT(5)
 
#define 	SDHCI_INTR_STS_BUFF_WRITE_READY   BIT(4)
 
#define 	SDHCI_INTR_STS_DMA   BIT(3)
 
#define 	SDHCI_INTR_STS_BLKGAP   BIT(2)
 
#define 	SDHCI_INTR_STS_TXR_COMPLETE   BIT(1)
 
#define 	SDHCI_INTR_STS_CMD_COMPLETE   BIT(0) /* CMD completed, CMD12/CMD23 will not generate this command */
 
#define 	SDHCI_INTR_ERR_TUNING   BIT(10)
 
#define 	SDHCI_INTR_ERR_ADMA   BIT(9)
 
#define 	SDHCI_INTR_ERR_AUTOCMD   BIT(8)
 
#define 	SDHCI_INTR_ERR_CURR_LIMIT   BIT(7)
 
#define 	SDHCI_INTR_ERR_DATA_ENDBIT   BIT(6)
 
#define 	SDHCI_INTR_ERR_DATA_CRC   BIT(5)
 
#define 	SDHCI_INTR_ERR_DATA_TIMEOUT   BIT(4)
 
#define 	SDHCI_INTR_ERR_CMD_INDEX   BIT(3)
 
#define 	SDHCI_INTR_ERR_CMD_ENDBIT   BIT(2)
 
#define 	SDHCI_INTR_ERR_CMD_CRC   BIT(1)
 
#define 	SDHCI_INTR_ERR_CMD_TIMEOUT   BIT(0)
 
#define 	SDHCI_INTR_ERR_CMD_LINE   (SDHCI_INTR_ERR_CMD_INDEX | SDHCI_INTR_ERR_CMD_ENDBIT | SDHCI_INTR_ERR_CMD_CRC | SDHCI_INTR_ERR_CMD_TIMEOUT)
 
#define 	SDHCI_INTR_ERR_DAT_LINE   (SDHCI_INTR_ERR_DATA_ENDBIT | SDHCI_INTR_ERR_DATA_CRC | SDHCI_INTR_ERR_DATA_TIMEOUT)
 
#define 	SDHCI_INTR_EN_ALL   (0x10FF)
 
#define 	SDHCI_ERR_EN_ALL   (0xF7FF)
 
#define 	SDHCI_INTR_SIG_EN   (SDHCI_INTR_STS_CARD_REMOVE | SDHCI_INTR_STS_CARD_INSERT | SDHCI_INTR_STS_CMD_COMPLETE | SDHCI_INTR_STS_TXR_COMPLETE)
 
#define 	SDHCI_INTR_SIGN_EN_SDMA   (SDHCI_INTR_SIG_EN | SDHCI_INTR_STS_DMA | SDHCI_INTR_STS_BLKGAP)
 
#define 	SDHCI_INTR_SIGN_EN_ADMA   (SDHCI_INTR_SIG_EN | SDHCI_INTR_STS_DMA)
 
#define 	SDHCI_INTR_SIGN_EN_PIO   (SDHCI_INTR_SIG_EN | SDHCI_INTR_STS_BLKGAP)
 
#define 	SDHCI_ERR_SIG_EN_ALL   (0xF3FF)
 
#define 	SDHCI_AUTOCMD12_ERR_NOT_EXECUTED   BIT(0)
 
#define 	SDHCI_AUTOCMD12_ERR_TIMEOUT   BIT(1)
 
#define 	SDHCI_AUTOCMD12_ERR_CRC   BIT(2)
 
#define 	SDHCI_AUTOCMD12_ERR_END_BIT   BIT(3)
 
#define 	SDHCI_AUTOCMD12_ERR_INDEX   BIT(4)
 
#define 	SDHCI_AUTOCMD12_ERR_CMD_NOT_ISSUE   BIT(7)
 
#define 	SDHCI_REG_HOST_CTRL2   0x3E
 
#define 	SDHCI_PRESET_VAL_EN   BIT(15)
 
#define 	SDHCI_ASYNC_INT_EN   BIT(14)
 
#define 	SDHCI_SMPL_CLCK_SELECT   BIT(7)
 
#define 	SDHCI_EXECUTE_TUNING   BIT(6) /* Write 1 Auto clear */
 
#define 	SDHCI_DRV_TYPE_MASK   BIT(4)
 
#define 	SDHCI_DRV_TYPE_SHIFT   4
 
#define 	SDHCI_DRV_TYPEB   0
 
#define 	SDHCI_DRV_TYPEA   1
 
#define 	SDHCI_DRV_TYPEC   2
 
#define 	SDHCI_DRV_TYPED   3
 
#define 	SDHCI_18V_SIGNAL   BIT(3)
 
#define 	SDHCI_UHS_MODE_MASK   (7 << 0)
 
#define 	SDHCI_SDR12   0
 
#define 	SDHCI_SDR25   1
 
#define 	SDHCI_SDR50   2
 
#define 	SDHCI_SDR104   3
 
#define 	SDHCI_DDR50   4
 
#define 	SDHCI_CAP_VOLTAGE_33V   BIT(24)
 
#define 	SDHCI_CAP_VOLTAGE_30V   BIT(25)
 
#define 	SDHCI_CAP_VOLTAGE_18V   BIT(26)
 
#define 	SDHCI_CAP_FIFO_DEPTH_16BYTE   (0 << 29)
 
#define 	SDHCI_CAP_FIFO_DEPTH_32BYTE   (1 << 29)
 
#define 	SDHCI_CAP_FIFO_DEPTH_64BYTE   (2 << 29)
 
#define 	SDHCI_CAP_FIFO_DEPTH_512BYTE   (3 << 29)
 
#define 	SDHCI_CAP_FIFO_DEPTH_1024BYTE   (4 << 29)
 
#define 	SDHCI_CAP_FIFO_DEPTH_2048BYTE   (5 << 29)
 
#define 	SDHCI_SUPPORT_SDR50   BIT(0)
 
#define 	SDHCI_SUPPORT_SDR104   BIT(1)
 
#define 	SDHCI_SUPPORT_DDR50   BIT(2)
 
#define 	SDHCI_SUPPORT_DRV_TYPEA   BIT(4)
 
#define 	SDHCI_SUPPORT_DRV_TYPEC   BIT(5)
 
#define 	SDHCI_SUPPORT_DRV_TYPED   BIT(6)
 
#define 	SDHCI_RETUNING_TIME_MAS   0xF
 
#define 	SDHCI_RETUNING_TIME_SHIFT   8
 
#define 	SDHCI_SDR50_TUNING   BIT(13)
 
#define 	SDCHI_RETUNING_MODE_MASK   0x3
 
#define 	SDHCI_RETUNING_MODE_SHIFT   14
 
#define 	MMC_BOOT_ACK   BIT(2)
 
#define 	MMC_BUS_TEST_MODE   0x3
 
#define 	MMC_ALTERNATIVE_BOOT_MODE   0x2
 
#define 	MMC_BOOT_MODE   0x1
 
#define 	NORMAL_MODE   0x0
 
#define 	SDHCI_CMD0_GO_IDLE_STATE   0
 
#define 	SDHCI_CMD1_MMC_SEND_OP_COND   1
 
#define 	SDHCI_CMD2_SEND_ALL_CID   2
 
#define 	SDHCI_CMD3_SEND_RELATIVE_ADDR   3
 
#define 	SDHCI_CMD5_IO_SEND_OP_COND   5
 
#define 	SDHCI_CMD6_SWITCH_FUNC   6
 
#define 	SDHCI_CMD6_SET_BUS_WIDTH   6
 
#define 	SDHCI_CMD7_SELECT_CARD   7
 
#define 	SDHCI_CMD8_SEND_IF_COND   8
 
#define 	SDHCI_CMD8_SEND_EXT_CSD   8
 
#define 	SDHCI_CMD9_SEND_CSD   9
 
#define 	SDHCI_CMD10_SEND_CID   10
 
#define 	SDHCI_CMD11_VOLTAGE_SWITCH   11
 
#define 	SDHCI_CMD12_STOP_TRANS   12
 
#define 	SDHCI_CMD13_SEND_STATUS   13
 
#define 	SDHCI_CMD13_SD_STATUS   13
 
#define 	SDHCI_CMD16_SET_BLOCKLEN   16
 
#define 	SDHCI_CMD17_READ_SINGLE_BLOCK   17
 
#define 	SDHCI_CMD18_READ_MULTI_BLOCK   18
 
#define 	SDHCI_CMD19_SEND_TUNE_BLOCK   19
 
#define 	SDHCI_CMD23_SET_WR_BLOCK_CNT   23
 
#define 	SDHCI_CMD24_WRITE_BLOCK   24
 
#define 	SDHCI_CMD25_WRITE_MULTI_BLOCK   25
 
#define 	SDHCI_CMD32_ERASE_WR_BLK_START   32
 
#define 	SDHCI_CMD33_ERASE_WR_BLK_END   33
 
#define 	SDHCI_CMD35_ERASE_GROUP_START   35
 
#define 	SDHCI_CMD36_ERASE_GROUP_END   36
 
#define 	SDHCI_CMD38_ERASE   38
 
#define 	SDHCI_CMD41_SD_SEND_OP_COND   41
 
#define 	SDHCI_CMD43_GET_MKB   43
 
#define 	SDHCI_CMD44_GET_MID   44
 
#define 	SDHCI_CMD45_CER_RN1   45
 
#define 	SDHCI_CMD46_CER_RN2   46
 
#define 	SDHCI_CMD47_CER_RES2   47
 
#define 	SDHCI_CMD48_CER_RES1   48
 
#define 	SDHCI_CMD51_SEND_SCR   51
 
#define 	SDHCI_CMD52_IO_RW_DIRECT   52
 
#define 	SDHCI_CMD53_IO_RW_EXTENDED   53
 
#define 	SDHCI_CMD55_APP   55
 
#define 	SDHCI_CMD56_GEN   56
 
#define 	SDHCI_CMD8_SEND_IF_COND_ARGU   0x1AA
 
#define 	SDHCI_CMD41_SD_SEND_OP_COND_HCS_ARGU   0xC0FF8000
 
#define 	SDHCI_CMD41_SD_SEND_OP_COND_ARGU   0x00FF8000
 
#define 	SDHCI_CMD1_MMC_SEND_OP_COND_BYTE_MODE   0x80FF8000
 
#define 	SDHCI_CMD1_MMC_SEND_OP_COND_SECTOR_MODE   0xC0FF8000
 
#define 	CMD_RETRY_CNT   5
 
#define 	SDHCI_TIMEOUT   0xFFF
 
#define 	SD_CMD52_RW_in_W   0x80000000
 
#define 	SD_CMD52_RW_in_R   0x00000000
 
#define 	SD_CMD52_RAW   0x08000000
 
#define 	SD_CMD52_no_RAW   0x00000000
 
#define 	SD_CMD52_FUNC(Num)   (Num << 28)
 
#define 	SD_CMD52_Reg_Addr(Addr)   (Addr << 9)
 
#define 	SD_CMD53_RW_in_W   0x80000000
 
#define 	SD_CMD53_RW_in_R   0x00000000
 
#define 	SD_CMD53_FUNC(Num)   (Num << 28)
 
#define 	SD_CMD53_Block_Mode   0x08000000
 
#define 	SD_CMD53_Byte_Mode   0x00000000
 
#define 	SD_CMD53_OP_inc   0x04000000
 
#define 	SD_CMD53_OP_fix   0x00000000
 
#define 	SD_CMD53_Reg_Addr(Addr)   (Addr << 9)
 
#define 	SD_STATUS_OUT_OF_RANGE   0x80000000
 
#define 	SD_STATUS_ADDRESS_ERROR   BIT(30)
 
#define 	SD_STATUS_BLOCK_LEN_ERROR   BIT(29)
 
#define 	SD_STATUS_ERASE_SEQ_ERROR   BIT(28)
 
#define 	SD_STATUS_ERASE_PARAM   BIT(27)
 
#define 	SD_STATUS_WP_VIOLATION   BIT(26)
 
#define 	SD_STATUS_CARD_IS_LOCK   BIT(25)
 
#define 	SD_STATUS_LOCK_UNLOCK_FAILED   BIT(24)
 
#define 	SD_STATUS_COM_CRC_ERROR   BIT(23)
 
#define 	SD_STATUS_ILLEGAL_COMMAND   BIT(22)
 
#define 	SD_STATUS_CARD_ECC_FAILED   BIT(21)
 
#define 	SD_STATUS_CC_ERROR   BIT(20)
 
#define 	SD_STATUS_ERROR   BIT(19)
 
#define 	SD_STATUS_UNDERRUN   BIT(18)
 
#define 	SD_STATUS_OVERRUN   BIT(17)
 
#define 	SD_STATUS_CSD_OVERWRITE   BIT(16)
 
#define 	SD_STATUS_WP_ERASE_SKIP   BIT(15)
 
#define 	SD_STATUS_CARD_ECC_DISABLE   BIT(14)
 
#define 	SD_STATUS_ERASE_RESET   BIT(13)
 
#define 	SD_STATUS_CURRENT_STATE   (0xF << 9)
 
#define 	SD_STATUS_READY_FOR_DATA   BIT(8)
 
#define 	MMC_STATUS_SWITCH_ERROR   BIT(7)
 
#define 	SD_STATUS_APP_CMD   BIT(5)
 
#define 	SD_STATUS_AKE_SEQ_ERROR   BIT(3)
 
#define 	SD_STATUS_ERROR_BITS
 
#define 	SDHCI_1BIT_BUS_WIDTH   0x0
 
#define 	SDHCI_4BIT_BUS_WIDTH   0x2
 
#define 	ADMA2_ENTRY_VALID   BIT(0)
 
#define 	ADMA2_ENTRY_END   BIT(1)
 
#define 	ADMA2_ENTRY_INT   BIT(2)
 
#define 	ADMA2_NOP   (0 << 4)
 
#define 	ADMA2_SET   (1 << 4)
 
#define 	ADMA2_TRAN   (2 << 4)
 
#define 	ADMA2_LINK   (3 << 4)
 
#define 	SDHCI_MMC_SWITCH   6
 
#define 	SDHCI_MMC_VENDOR_CMD   62
 
#define 	EXT_CSD_CMD_SET_NORMAL   (1<<0)
 
#define 	EXT_CSD_CMD_SET_SECURE   (1<<1)
 
#define 	EXT_CSD_CMD_SET_CPSECURE   (1<<2)
 
#define 	EXT_CSD_PARTITION_SETTING_COMPLETED   156
 
#define 	EXT_CSD_PARTITION_CONF   179
 
#define 	EXT_CSD_BUS_WIDTH   183 /* R/W */
 
#define 	EXT_CSD_HS_TIMING   185 /* R/W */
 
#define 	EXT_CSD_CARD_TYPE   196 /* RO */
 
#define 	EXT_CSD_SEC_CNT   212 /* RO, 4 bytes */
 
#define 	EXT_CSD_BOOT_SIZE_MULT   226
 
#define 	EXT_CSD_CMD_SET   0x0
 
#define 	EXT_CSD_SET_BIT   0x1
 
#define 	EXT_CSD_CLR_BYTE   0x2
 
#define 	EXT_CSD_WRITE_BYTE   0x3
 
#define 	EXT_CSD_BUS_8BIT   0x2
 
#define 	EXT_CSD_BUS_4BIT   0x1
 
#define 	EXT_CSD_BUS_1BIT   0x0
 
#define 	MMC_CMD6_ACCESS_MODE(x)   (uint32_t)( x << 24)
 
#define 	MMC_CMD6_INDEX(x)   (uint32_t)( x << 16)
 
#define 	MMC_CMD6_VALUE(x)   (uint32_t)( x << 8)
 
#define 	MMC_CMD6_CMD_SET(x)   (uint32_t)( x )
 
#define 	MMC_CARD_BUSY   0x80000000 /* Card Power up status bit */
```

### Enumerations
```
enum  	kdrv_sdc_dev_e { KDRV_SDC0_DEV = 0, KDRV_SDC1_DEV }
 
enum  	kdrv_sdc_infinite_test_e { INFINITE_NO = 0, INFINITE_MODE_1, INFINITE_MODE_2 }
 
enum  	kdrv_sdc_transfer_act_e { WRITE = 0, READ }
 
enum  	kdrv_sdc_transfer_type_e {
		ADMA = 0, SDMA, PIO, EDMA,
		TRANS_UNKNOWN
}
 
enum  	kdrv_sdc_abort_type_e { ABORT_ASYNCHRONOUS = 0, ABORT_SYNCHRONOUS, ABORT_UNDEFINED }
 
enum  	kdrv_sdc_cprm_test_e { CPRM_PROTECT_RW, CPRM_FILESYS, CPRM_UNKNOWN }
 
enum  	kdrv_sdc_bus_speed_e {
		SPEED_DEFAULT = 0, SPEED_SDR25, SPEED_SDR50, SPEED_SDR104,
		SPEED_DDR50, SPEED_RSRV
}
 
enum  	kdrv_sdc_card_state_e {
		CUR_STATE_IDLE = 0, CUR_STATE_READY, CUR_STATE_IDENT, CUR_STATE_STBY,
		CUR_STATE_TRAN, CUR_STATE_DATA, CUR_STATE_RCV, CUR_STATE_PRG,
		CUR_STATE_DIS, CUR_STATE_RSV
}
```

### Functions
```
kdrv_status_t kdrv_sdc_dev_scan	(	kdrv_sdc_dev_e 	dev_id	)

kdrv_sdc_dev_scan() scan sd/mmc memory card

Parameters
	in]	dev_id	device id, ref @kdrv_sdc_dev_e
Returns
	kdrv_status_t
```
```
kdrv_sdc_res_t* kdrv_sdc_get_dev	(	kdrv_sdc_dev_e 	dev_id	)

kdrv_sdc_get_dev() get device structure

Parameters
	[in]	dev_id	device id, ref @kdrv_sdc_dev_e
Returns
	kdrv_status_t
```
```
kdrv_status_t kdrv_sdc_initialize	(	kdrv_sdc_dev_e 	dev_id	)	

kdrv_sdc_initialize, initail sd/emmc card interface
1. reset sdc status
2. allocate resource and initail driving
3. turn on sdc clock

Parameters
	[in]	dev_id	device id, ref @kdrv_sdc_dev_e
Returns
	kdrv_status_t
```
```
kdrv_status_t kdrv_sdc_read	(	kdrv_sdc_dev_e 	dev_id,
								uint8_t * 	buf,
								uint32_t 	sd_offset,
								uint32_t 	size 
							)		
kdrv_sdc_read read data from sd/mmc card

Parameters
	[in]	dev_id	device id, ref @kdrv_sdc_dev_e
	[in]	buf	buffer to write.
	[in]	sd_offset	sd/mmc offset address
	[in]	size	read size(Multiple of 512, 1sector=512Bytes, max block 65535 ~ 3MB)
Returns
	kdrv_status_t
```
```
kdrv_status_t kdrv_sdc_uninitialize	(	kdrv_sdc_dev_e 	dev_id	)

kdrv_sdc_uninitialize, uninitail sd/emmc card interface and resource
1. reset sdc status and initail driven
2. turn on sdc clock
Parameters
	[in]	dev_id	device id, ref @kdrv_sdc_dev_e
Returns
	kdrv_status_t
```
```
kdrv_status_t kdrv_sdc_write	(	kdrv_sdc_dev_e 	dev_id,
									uint8_t * 	buf,
									uint32_t 	sd_offset,
									uint32_t 	size 
								)		
kdrv_sdc_write write data from sd/mmc card

Parameters
	[in]	dev_id	device id, ref @kdrv_sdc_dev_e
	[in]	buf	buffer to write.
	[in]	sd_offset	sd/mmc offset address
	[in]	size	write size(Multiple of 512, 1sector=512Bytes, max block 65535 ~ 3MB)
Returns
	kdrv_status_t
```

## KDRV_SPIF_NOR
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Macros
```
#define 	MEMXFER_OPS_NONE   0x00
 
#define 	MEMXFER_OPS_CPU   0x01
 
#define 	MEMXFER_OPS_DMA   0x02
 
#define 	MEMXFER_INITED   0x10
 
#define 	MEMXFER_OPS_MASK   MEMXFER_OPS_CPU | MEMXFER_OPS_DMA
```

### Functions
```
void kdrv_spif_initialize	(	void 		)	

Initialize spi flash include hardware setting, operation frequency, and flash status check.

Parameters
	[in]	N/A	
Returns
	N/A
Note
	This API MUST be called before using the Read/write APIs for spi flash.
```
```
void kdrv_spif_memxfer_initialize	(	uint8_t 	flash_mode,
										uint8_t 	mem_mode 
									)		
Initialize spi flash for memxfer include hardware setting, operation frequency, and flash status check.

Parameters
	[in]	flash_mode	flash operating mode
	[in]	mem_mode	memory operating mode
Returns
	N/A
```
```
kdrv_status_t kdrv_spif_uninitialize	(	void 		)	

Uninitialize spi flash and clear related variables.

Parameters
		[in]	N/A	
Returns
	kdrv_status_t
```
```
void kdrv_spif_set_commands	(	uint32_t 	cmd0,
								uint32_t 	cmd1,
								uint32_t 	cmd2,
								uint32_t 	cmd3 
							)		
set spi communication commands including read/write by 3/4bytes address, dummy byte size, operation mode, etc

Parameters
	[in]	cmd0	~ 3
Returns
	N/A
```
```
void kdrv_spif_wait_command_complete	(	void 		)	

Check status bit to wait until command completed.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_wait_rx_full	(	void 		)

Wait until the RX FIFO is full so ready to read.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_wait_tx_empty	(	void 		)	

Wait until the TX FIFO is empty so ready to write.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
uint32_t kdrv_spif_rxfifo_depth	(	void 		)

Check the RX FIFO size, unit in byte.

Parameters
	[in]	N/A	
Returns
	>0 RX FIFO depth
```
```
uint32_t kdrv_spif_txfifo_depth	(	void 		)	

Check the TX FIFO size, unit in byte.

Parameters
	[in]	N/A	
Returns
	>0 TX FIFO depth
```
```
void kdrv_spif_read_data	(	uint32_t * 	buf,
								uint32_t 	length 
							)		
read data from specific index in spi flash

Parameters
	[in]	*buf	buffer for the data read from flash
	[in]	length	data size
Returns
	N/A
```
```
void kdrv_spif_write_data	(	uint8_t * 	buf,
								uint32_t 	length 
							)		
write data to specific index in spi flash

Parameters
	[in]	*buf	buffer for the data to write to flash
	[in]	length	data size
Returns
	N/A
```
```
void kdrv_spif_read_Rx_FIFO	(	uint32_t * 	buf_word,
								uint16_t * 	buf_word_index,
								uint32_t 	target_byte 
							)		
read Rx FIFO data

Parameters
	[in]	*buf_word	buffer for the data read from flash
	[in]	*buf_word_index	start from specific flash index
	[in]	target_byte	data size
Returns
	N/A
```
```
void kdrv_spif_check_status_till_ready_2	(	void 		)	

check status till the progress is done and ready for next step

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_check_status_till_ready	(	void 		)

wait command completed and check status till it's ready

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_check_quad_status_till_ready	(	void 		)

wait quad read command completed and check status till ready

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_pre_log	(	void 		)	

to remeber the original settings for SPI flash

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_switch_org	(	void 		)	

to switch back to original SPI flash settings

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_switch_low_speed	(	void 		)	

to switch to low speed (50Mhz) SPI flash settings

Parameters
	[in]	N/A	
Returns
	N/A
```

## KDRV_SPIF_NAND
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Macros
```
#define 	MEMXFER_OPS_NONE   0x00
 
#define 	MEMXFER_OPS_CPU   0x01
 
#define 	MEMXFER_OPS_DMA   0x02
 
#define 	MEMXFER_INITED   0x10
 
#define 	MEMXFER_OPS_MASK   MEMXFER_OPS_CPU | MEMXFER_OPS_DMA
```

### Functions
```
void kdrv_spif_check_quad_status_till_ready	(	void 		)	

wait quad read command completed and check status till ready

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_check_status_till_ready	(	void 		)	

wait command completed and check status till it's ready

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_check_status_till_ready_2	(	void 		)
	
check status till the progress is done and ready for next step

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_initialize	(	void 		)

Initialize spi flash include hardware setting, operation frequency, and flash status check.

Parameters
	[in]	N/A	
Returns
	N/A
Note
	This API MUST be called before using the Read/write APIs for spi flash.
```
```
void kdrv_spif_memxfer_initialize	(	uint8_t 	flash_mode,
										uint8_t 	mem_mode 
									)		
Initialize spi flash for memxfer include hardware setting, operation frequency, and flash status check.

Parameters
	[in]	flash_mode	flash operating mode
	[in]	mem_mode	memory operating mode
Returns
	N/A
```
```
void kdrv_spif_pre_log	(	void 		)	

to remeber the original settings for SPI flash

Parameters
	[in]	N/A	
Returns
	N/A
```
```

void kdrv_spif_read_data	(	uint32_t * 	buf,
								uint32_t 	length 
							)		
read data from specific index in spi flash

Parameters
	[in]	*buf	buffer for the data read from flash length data size
Returns
	N/A
```
```
void kdrv_spif_read_Rx_FIFO	(	uint32_t * 	buf_word,
								uint16_t * 	buf_word_index,
								uint32_t 	target_byte 
							)		
read Rx FIFO data

Parameters
	[in]	*buf_word	buffer for the data read from flash
	[in]	*buf_word_index	start from specific flash index
	[in]	target_byte	data size
Returns
	N/A
```
```
uint32_t kdrv_spif_rxfifo_depth	(	void 		)	

Check the RX FIFO size, unit in byte.

Parameters
	[in]	N/A	
Returns
	>0 RX FIFO depth
```
```
void kdrv_spif_set_commands	(	uint32_t 	cmd0,
								uint32_t 	cmd1,
								uint32_t 	cmd2,
								uint32_t 	cmd3 
							)		
set spi communication commands including read/write by 3/4bytes address, dummy byte size, operation mode, etc

Parameters
	[in]	cmd0	~ 3
Returns
	N/A
```
```
void kdrv_spif_switch_low_speed	(	void 		)	

to switch to low speed (50Mhz) SPI flash settings

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_switch_org	(	void 		)

to switch back to original SPI flash settings

Parameters
	[in]	N/A	
Returns
	N/A
```
```
uint32_t kdrv_spif_txfifo_depth	(	void 		)	

Check the TX FIFO size, unit in byte.

Parameters
	[in]	N/A	
Returns
	>0 TX FIFO depth
```
```
kdrv_status_t kdrv_spif_uninitialize	(	void 		)

Uninitialize spi flash and clear related variables.

Parameters
	[in]	N/A	
Returns
	kdrv_status_t
```
```
void kdrv_spif_wait_command_complete	(	void 		)	

Check status bit to wait until command completed.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_wait_rx_full	(	void 		)	

Wait until the RX FIFO is full so ready to read.

Parameters
	[in]	N/A	
Returns
	N/A
```
```
void kdrv_spif_wait_tx_empty	(	void 		)

Wait until the TX FIFO is empty so ready to write.

Parameters
	[in]	N/A	
Returns
	N/A
```
```

void kdrv_spif_write_data	(	uint8_t * 	buf,
								uint32_t 	length 
							)		
write data to specific index in spi flash

Parameters
	[in]	*buf	buffer for the data to write to flash
	[in]	length	data size
Returns
	N/A
```
```
void kdrv_spif_write_data_nand	(	uint8_t 	type,
									uint32_t 	dst,
									uint8_t * 	buf,
									uint32_t 	length 
								)		
write data to specific index in spi flash

Parameters
	[in]	type	Normal program or Quad program
	[in]	dst	program destination address
	[in]	*buf	buffer for the data to write to flash
	[in]	length	data size
Returns
	N/A
```

## KDRV_SYSTEM
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Macros
```
#define 	FLAGS_SOURCE_READY_EVT   0x91ad
 
#define 	SCPU_FW   1
 
#define 	NCPU_FW   2
```

### Enumerations
```
anonymous enum

Enumeration of system reset.

| Enumerator     												|
| SUBSYS_NPU 	| Enum 1, Software reset for NPU				|
| SUBSYS_PD_NPU | Enum 2, Software reset for whole NPU domain	|
| SUBSYS_LCDC 	| Enum 3, Software reset for LCDC				|
| SUBSYS_NCPU 	| Enum 4, The signal controls SYSRESETn of NCPU	|
| GLOBAL_RESET 	| Enum 5										|
```

### Functions
```
void kdrv_system_init_ncpu	(	void 		)	

NCPU system initialize.
Enable NCPU/NPU and some main PLL clock .

Returns
	N/A
Note
	This API should be called after kdrv_system_initialize() to make sure NPU/DDR power domain is powered on.
```
```
void kdrv_system_initialize	(	void 		)

System initialize.
Turn on NPU/DDR power domain and enable some main clock PLL .

Returns
	N/A
```
```
void kdrv_system_reset	(	int32_t 	subsystem	)	

System reset.

Parameters
	[in]	subsystem	subsystem reset id
Note
	SUBSYS_NPU: reset NPU
	SUBSYS_PD_NPU: reset whole NPU domain(clk+ddr phy)
	SUBSYS_LCDC: reset LCDC
	SUBSYS_NCPU: reset NCPU
Returns
	N/A
```

## KDRV_TIMER
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Enumerations
```
enum cb_event_t

Enumerations of all timer call back even return status.

| Enumerator     										|
| TIMER_M1_TIMEOUT 	| Enum 0, reach timer M1 level		|
| TIMER_M2_TIMEOUT 	| Enum 1, reach timer M2 level		|
| TIMER_OF_TIMEOUT 	| Enum 2, timer overfloor			|
```
```
enum timer_clksource_t

Enumerations of all clock source option for timer_clksource_t.

| Enumerator     													|
| TIMER_CLKSOURCE_PCLK 		| Enum 0, clock source from pclk		|
| TIMER_CLKSOURCE_EXTCLK 	| Enum 1, clock source from ext clock	|
```
```
enum timer_stat_t

Enumerations of all timer status for kdrv_timer_set.

| Enumerator     													|
| TIMER_PAUSE 			| Enum 0, Pause timer						|
| TIMER_START 			| Enum 1, Start timer						|
| TIMER_STAT_DEFAULT 	| Enum 2, Start timer with default setting	|
```

### Functions
```
kdrv_status_t kdrv_timer_close	(	uint32_t * 	TimerId	)

Close specific timer id.

Parameters
	[in]	TimerId	pointer of timer id
Returns
	kdrv_status_t see kdrv_status_t
```
```
Let system delay ms.

Parameters
	[in]	usec	time interval(ms).
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_timer_delay_ms_long	(	uint32_t 	msec	)

Let system delay ms.

Parameters
	[in]	usec	time interval(ms).
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_timer_delay_us	(	uint32_t 	usec	)	

Let system delay us.

Parameters
	[in]	usec	time interval(us).
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_timer_initialize	(	void 		)	

Enable clock, init timer ip, register IRQ/ISR function.

Parameters
	[in]	N/A	
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_timer_open	(	uint32_t * 	TimerId,
									timer_cb_fr_isr_t 	cb_event,
									void * 	arg,
									timer_clksource_t 	clksource_opt 
								)		
Request one timer id for further usage.

Parameters
	[out]	TimerId	pointer of timer id.
	[in]	event_cb	timer_cb_fr_isr_t, see timer_cb_fr_isr_t
	[in]	arg	user define argument
	[in]	clksource_opt	clock source option, see timer_clksource_t
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_timer_perf_get_instant	(	uint32_t * 	TimerId,
												uint32_t * 	instant,
												uint32_t * 	time 
											)		
Get time consumption.

Parameters
	[in]	TimerId	pointer of timer id
	[out]	instant	pointer of time instant register
Returns
	Time cunsumption
```
```
kdrv_status_t kdrv_timer_perf_measure_get_us	(	uint32_t * 	diff,
													uint32_t * 	currt_cnt 
												)		
Get time interval.

Parameters
	[in]	diff	Difference time interval compare to last time instant.
	[in]	currt_cnt	Current counter.
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_timer_perf_measure_start	(	void 		)	

Start to use performance measurement function.

Parameters
	[in]	N/A	
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_timer_perf_open	(	uint32_t * 	TimerId	)	

Open a timer with specific timer id for performance measurement.

Note
	Need use kdrv_timer_perf_set() to start timing measurement.
Parameters
	[out]	TimerId	pointer of timer id
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_timer_perf_reset	(	uint32_t * 	TimerId	)	

Reset performance timer.

Parameters
	[in]	TimerId	pointer of timer id
Returns
	kdrv_status_t see kdrv_status_t
Note
	After call kdrv_timer_perf_open(), you should reset this timer first.
Example:
	uint32_t perftimerid; kdrv_timer_perf_open(&pftimerid);
	kdrv_timer_perf_reset(&pftimerid);
```
```
kdrv_status_t kdrv_timer_perf_set	(	uint32_t * 	TimerId	)	

Set specific timer for performance measurment usage.

Parameters
	[in]	TimerId	pointer of timer id
Returns
	kdrv_status_t see kdrv_status_t
Note
	You should call kdrv_timer_perf_open() and kdrv_timer_perf_reset() firstly before call this API.
Example:
	uint32_t perftimerid;
	kdrv_timer_perf_open(&pftimerid);
	kdrv_timer_perf_reset(&pftimerid);
	kdrv_timer_perf_set(&perftimerid);
```
```
kdrv_status_t kdrv_timer_set	(	uint32_t * 	TimerId,
									uint32_t 	Intval,
									timer_stat_t 	State 
								)		
Set specific timer with interval and status.

Parameters
	[in]	TimerId	pointer of timer id
	[in]	Interval	set timer interval
	[in]	timer_stat	see timer_stat, see timer_stat_t
Returns
	kdrv_status_t see kdrv_status_t
Note
	This API should be called after kdrv_timer_open()
Example:
	uint32_t timerid;
	kdrv_timer_open(&timerid, NULL, NULL);
	kdrv_timer_set(&timerid, 5000000, TIMER_START);
```
```
kdrv_status_t kdrv_timer_uninitialize	(	void 		)	

Disable clock, and timer IRQ.

Parameters
	[in]	N/A	
Returns
	kdrv_status_t see kdrv_status_t
```

## KDRV_UART
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Data Structure
```
struct  	kdrv_uart_rbr_t
			Structure of Receiver Buffer Register (RBR , Offset: 0x00 for Read) More...
 
struct  	kdrv_uart_thr_t
			Structure of Transmitter Holding Register (THR , Offset: 0x00 for Write) More...
 
struct  	kdrv_uart_ier_t
			Structure of Interrupt Enable Register (IER , Offset: 0x04) More...
 
struct  	kdrv_uart_iir_t
			Structure of Interrupt Identification Register (IIR , Offset: 0x08 Read_Only) More...
 
struct  	kdrv_uart_fcr_t
			Structure of FIFO Control Register (FCR , Offset: 0x08 for Write) More...
 
struct  	kdrv_uart_lcr_t
			Structure of Line Control Register (LCR Offset: 0x0C) More...
 
struct  	kdrv_uart_mcr_t
 
struct  	kdrv_uart_lsr_t
 
struct  	kdrv_uart_tst_t
 
struct  	kdrv_uart_msr_t
			Structure of Modem Status Register (MSR , Offset: 0x18) More...
 
struct  	kdrv_uart_spr_t
			Structure of Scratch Pad Register (SPR , Offset: 0x1C) More...
 
struct  	kdrv_uart_mdr_t
			Structure of Mode Definition Register (MDR , O ffset: 0x20) More...
 
struct  	kdrv_uart_feature_t
			Structure of Feature Register (Feature, O ffset: 0x68) More...
 
struct  	kdrv_uart_dll_t
			Structure of Baud Rate Divisor Latch LSB (DLL, Offset: 0x00 when DLAB = 1) More...
 
struct  	kdrv_uart_dlm_t
			Structure of Baud Rate Divisor Latch MSB (DLM, Offset: 0x04 when DLAB = 1) More...
 
struct  	kdrv_uart_psr_t
			Structure of Prescaler Register (PSR , Offset: 0x 08 when DLAB = 1) More...
 
union  		U_regUART_ctrl
 
union  		U_regUART_feature
 
union  		U_regUART_baudrate
 
struct  	kdrv_uart_config_t
			Structure of UART configuration parameters. More...
 
struct  	kdrv_uart_fifo_config_t
			Structure of UART FIFO configuration parameters. More...
```

### Macros
```
#define 	regUART0_ctrl   ((volatile U_regUART_ctrl *)UART0_REG_BASE)
 
#define 	regUART0_baudrate   ((volatile U_regUART_baudrate *)UART0_REG_BASE)
 
#define 	regUART0_feature   ((volatile U_regUART_feature *)(UART0_REG_BASE+0x68))
 
#define 	regUART1_ctrl   ((volatile U_regUART_ctrl *)UART1_REG_BASE)
 
#define 	regUART1_baudrate   ((volatile U_regUART_baudrate *)UART1_REG_BASE)
 
#define 	regUART1_feature   ((volatile U_regUART_feature *)(UART1_REG_BASE+0x68))
 
#define 	regUART_ctrl(n)   ((volatile U_regUART_ctrl *)(UART0_REG_BASE+(n*0x100000)))
 
#define 	regUART_baudrate(n)   ((volatile U_regUART_baudrate *)(UART0_REG_BASE+(n*0x100000)))
 
#define 	regUART_feature(n)   ((volatile U_regUART_feature *)(UART0_REG_BASE+(n*0x100000)+0x68))
 
#define 	BAUD_921600   (UART_CLOCK / 14745600)
			Enumerations of UART baud rate. More...
 
#define 	BAUD_460800   (UART_CLOCK / 7372800)
 
#define 	BAUD_115200   (UART_CLOCK / 1843200)
 
#define 	BAUD_57600   (UART_CLOCK / 921600)
 
#define 	BAUD_38400   (UART_CLOCK / 614400)
 
#define 	BAUD_19200   (UART_CLOCK / 307200)
 
#define 	BAUD_14400   (UART_CLOCK / 230400)
 
#define 	BAUD_9600   (UART_CLOCK / 153600)
 
#define 	BAUD_4800   (UART_CLOCK / 76800)
 
#define 	BAUD_2400   (UART_CLOCK / 38400)
 
#define 	BAUD_1200   (UART_CLOCK / 19200)
```

### Enumerations
```
enum DRVUART_PORT

Enumerations of UART port parameters.

| Enumerator     								|
| DRVUART_PORT0 	| Enum 0, UART port 0		|
| DRVUART_PORT1 	| Enum 1, UART port 1		|
```
```
enum kdrv_uart_control_t

Enumerations of UART control hardware signals

| Enumerator     												|
| UART_CTRL_CONFIG 		| Enum 0, set kdrv_uart_config_t		|
| UART_CTRL_FIFO_RX 	| Enum 1, set kdrv_uart_fifo_config_t	|
| UART_CTRL_FIFO_TX 	| Enum 2, set kdrv_uart_fifo_config_t	|
| UART_CTRL_LOOPBACK 	| Enum 3, UART loopback enable			|
| UART_CTRL_TX_EN 		| Enum 4, UART transmitter enable		|
| UART_CTRL_RX_EN 		| Enum 5, UART receiver enable			|
| UART_CTRL_ABORT_TX 	| Enum 6, UART abort transmitter		|
| UART_CTRL_ABORT_RX 	| Enum 7, UART abort receiver			|
| UART_CTRL_TIMEOUT_RX 	| Enum 8, UART receiver timeout value	|
| UART_CTRL_TIMEOUT_TX 	| Enum 9, UART transmitter timeout value|
```
```
enum kdrv_uart_dev_id_t

Enumerations of UART device instance parameters.

| Enumerator     											|
| UART0_DEV 		| Enum 0, UART device instance 0		|
| UART1_DEV 		| Enum 1, UART device instance 1		|
| TOTAL_UART_DEV 	| Enum 2, Total UART device instances	|
```
```
enum kdrv_uart_mode_t

Enumerations of UART mode parameters.

| Enumerator     														|
| UART_MODE_ASYN_RX 	| Enum 0x1,UART asynchronous receiver mode.		|
| UART_MODE_ASYN_TX 	| Enum 0x2,UART asynchronous transmitter mode.	|
| UART_MODE_SYNC_RX 	| Enum 0x4,UART synchronous receiver mode.		|
| UART_MODE_SYNC_TX 	| Enum 0x8,UART synchronous transmitter mode.	|
```
```
enum kdrv_uart_parity_t

Enumerations of UART parity.

| Enumerator     								|
| PARITY_NONE 	| Enum 0, Disable Parity		|
| PARITY_ODD 	| Enum 1,Odd Parity				|
| PARITY_EVEN 	| Enum 2, Even Parity			|
| PARITY_MARK 	| Enum 3, Stick odd Parity		|
| PARITY_SPACE 	| Enum 4, Stick even Parity		|
```

### Functions
```
kdrv_status_t kdrv_uart_close	(	kdrv_uart_handle_t 	handle	)
	
close the UART port

Parameters
	[in]	handle	device handle for an UART port
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_uart_configure	(	kdrv_uart_handle_t 	handle,
										kdrv_uart_control_t 	prop,
										uint8_t * 	val 
									)		
set control for the opened UART port

Parameters
	[in]	handle	device handle for an UART port
	[in]	prop	control enumeration
	[in]	val	pointer to control value/structure
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_uart_console_init	(	uint8_t 	uart_dev,
											uint32_t 	baudrate 
										)		
uart debug console port init

Parameters
	[in]	uart_dev	uart device id, kdrv_uart_dev_id_t
	[in]	baudrate	uart baud rate
Returns
	uart initialize status, see kdrv_status_t
```
```
kdrv_status_t kdrv_uart_get_char	(	kdrv_uart_handle_t 	handle,
										char * 	ch 
									)		
read character data from UART port

Parameters
	[in]	handle	device handle for an UART port
	[out]	ch	character data
Returns
	kdrv_status_t see kdrv_status_t
```
```
uint32_t kdrv_uart_get_rx_count	(	kdrv_uart_handle_t 	handle	)	

get char number in RX buffer

Parameters
	[in]	handle	device handle for an UART port
Returns
	number of RX count in the buffer
```
```
uint32_t kdrv_uart_get_tx_count	(	kdrv_uart_handle_t 	handle	)	

get char number in TX buffer

Parameters
	[in]	handle	device handle for an UART port
Returns
	number of TX count in the buffer
```
```
kdrv_status_t kdrv_uart_initialize	(	void 		)	

UART driver initialization, it shall be called once in lifecycle.

Returns
	kdrv_status_t see kdrv_status_t
```
```

kdrv_status_t kdrv_uart_open	(	kdrv_uart_handle_t * 	handle,
									uint8_t 	com_port,
									uint32_t 	mode,
									kdrv_uart_callback_t 	callback 
								)		
Open one UART port and acquire a uart port handle.

This API will open a UART device (com_port: 0-5) for use.
It will return a UART device handle for future device reference.
The client can choose work mode: asynchronization or synchronization.
Synchronization mode will poll the hardware status to determine send/receiving point,
it will consume more power and introduce more delay to system execution.
But in the case of non-thread light weight environment, such as message log function, this mode is easy and suitable.
Asynchronization mode lets the driver interrupt driven, save more system power and more efficient,
the client needs to have a thread to listen/wait for the event/signal sent from callback function.
Callback function parameter 'callback' will be registered with this device which is mandatory for async mode,
will be invoked whenever Tx/Rx complete or timeout occur.
This callback function should be very thin, can only be used to set flag or send signals

Parameters
	[out]	handle	a handle of an UART port
	[in]	com_port	UART port id
	[in]	mode	bit combination of kdrv_uart_mode_t
	[in]	callback	user callback function
Returns
	kdrv_status_t see kdrv_status_t
```
```

kdrv_status_t kdrv_uart_read	(	kdrv_uart_handle_t 	handle,
									uint8_t * 	buf,
									uint32_t 	len 
								)		
read data from the UART port

The client can call this API to receive UART data from remote side.
Depending on the work mode, a little bit different behavior exists there.
In synchronous mode, the API call will not return until all data was received physically.
In asynchronous mode, the API call shall return immediately with UART_API_RX_BUSY.
When enough bytes are received or timeout occurs, the client registered callback function will be invoked.
The client shall have a very thin code there to set flags/signals. The client thread shall be listening the signal after this API call.
The client shall allocate the receiving buffer with max possible receiving length.
When one frame is sent out, after 4 chars transmission time, a timeout interrupt will be generated.

Parameters
	[in]	handle	device handle for an UART port
	[out]	buf	data buffer
	[in]	len	data buffer length
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_uart_uninitialize	(	void 		)	

UART driver uninitialization.

Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_uart_write	(	kdrv_uart_handle_t 	hdl,
									uint8_t * 	buf,
									uint32_t 	len 
								)		
write data to uart port, such as command, parameters, but not suitable for chunk data

The client calls this API to send data out to remote side.
Depending on the work mode, a little bit different behavior exists there.
In synchronous mode, the API call will not return until all data was sent out physically;
In asynchronous mode, the API call shall return immediately with UART_API_TX_BUSY.
When all the buffer data is sent out, the client registered callback function will be invoked.
The client shall have a very thin code there to set flags/signals. The client thread shall be listening the signal after this API call.

Parameters
	[in]	handle	device handle for an UART port
	[in]	buf	data buffer
	[in]	len	data buffer length
Returns
	kdrv_status_t see kdrv_status_t
```

## KDRV_USBD3
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Macros
```
#define 	MAX_USBD3_ENDPOINT   4
```

### Enumerations
```
enum kdrv_usbd3_speed_t

Enumerations of all usb3 speed

| Enumerator     										|
| USBD3_NO_LINK_SPEED 	| Enum 0, USB3 no link speed	|
| USBD3_HIGH_SPEED 		| Enum 1, USB3 high speed		|
| USBD3_SUPER_SPEED 	| Enum 2, USB3 super speed		|
```
```
enum kdrv_usbd3_speed_t

Enumerations of all usb3 speed

| Enumerator     										|
| USBD3_NO_LINK_SPEED 	| Enum 0, USB3 no link speed	|
| USBD3_HIGH_SPEED 		| Enum 1, USB3 high speed		|
| USBD3_SUPER_SPEED 	| Enum 2, USB3 super speed		|
```

### Functions
```
kdrv_status_t kdrv_usbd3_bulk_receive	(	uint8_t 	endpoint,
											void * 	buf,
											uint32_t * 	blen,
											uint32_t 	timeout_ms 
										)		
Bulk-OUT transfser, receive data from the host through a bulk-out endpoint in blocking mode.

Parameters
	[in]	endpoint	a bulk-out endpoint address, should be the value from bEndpointAddress
	[out]	buf	buffer for receiving data
	[in,out]	blen	buffer length for input, actual transfered length for output
	[in]	timeout_ms	timeout in millisecond
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbd3_bulk_receive_zlp	(	uint8_t 	endpoint	)	

Bulk-OUT transfser, receive zip data from the host through a bulk-out endpoint in blocking mode.

Parameters
	[in]	endpoint	a bulk-out endpoint address, should be the value from bEndpointAddress
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbd3_bulk_send	(	uint8_t 	endpoint,
										void * 	buf,
										uint32_t 	txlen,
										uint32_t 	timeout_ms 
									)		
Bulk-IN transfser, send data to the host through a bulk-in endpoint in blocking mode.

Parameters
	[in]	endpoint	a bulk-in endpoint address, should be the value from bEndpointAddress
	[out]	buf	buffer for sending data
	[in]	txlen	data length to be sent
	[in]	timeout_ms	timeout in millisecond
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_usbd3_speed_t kdrv_usbd3_get_link_speed	(	void 		)	

Get USB3 link speed.

Parameters
	[in]	N/A	
Returns
	kdrv_usbd3_speed_t see kdrv_usbd3_speed_t
```
```
kdrv_usbd3_link_status_t kdrv_usbd3_get_link_status	(	void 		)	

Get USB3 link status.

Parameters
	[in]	N/A	
Returns
	kdrv_usbd3_link_status_t see kdrv_usbd3_link_status_t
```
```
kdrv_status_t kdrv_usbd3_initialize	(	kdrv_usbd3_HS_descriptors_t * 	hs_descs,
										kdrv_usbd3_SS_descriptors_t * 	ss_descs,
										kdrv_usbd3_link_status_callback_t 	status_isr_cb,
										kdrv_usbd3_user_control_callback_t 	usr_cx_isr_cb 
									)		
USB3 device mode driver initialization.

Parameters
	[in]	hs_descs	user created HS device descriptor, this must be kept during device enumeration, see kdrv_usbd3_HS_descriptors_t
	[in]	ss_descs	user created SS device descriptor, this must be kept during device enumeration, see kdrv_usbd3_SS_descriptors_t
	[in]	status_isr_cb	USBD event callback function, can be NULL, see kdrv_usbd3_link_status_callback_t
	[in]	usr_cx_isr_cb	see kdrv_usbd3_user_control_callback_t
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbd3_interrupt_send	(	uint32_t 	endpoint,
											void * 	buf,
											uint32_t 	txLen,
											uint32_t 	timeout_ms 
										)		
Interrupt transfser.

Parameters
	[in]	endpoint	a bulk-in endpoint address, should be the value from bEndpointAddress
	[out]	buf	buffer for sending data
	[in]	txlen	data length to be sent
	[in]	timeout_ms	timeout in millisecond
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbd3_reset_device	(	void 		)	

Reset USB3 device.

Parameters
	[in]	N/A	
Note
	this cannot be called in ISR context
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbd3_reset_endpoint	(	uint8_t 	endpoint	)

Reset USB3 endpoint.

Parameters
	[in]	N/A	
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbd3_set_enable	(	bool 	enable	)	

set enable/disabale of USB device mode, host can enumerate this device only if device is enabled

Parameters
	[in]	enable	true to enable, false to disable
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbd3_uninitialize	(	void 		)	

USB3 device mode driver de-initialization.

Parameters
	[in]	N/A	
Returns
	kdrv_status_t see kdrv_status_t
```

## KDRV_USBH2
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Data Structures
```
_ARM_USBH_PORT_STATE Struct Reference

Data Fields
uint32_t 	connected: 1
uint32_t 	overcurrent: 1
uint32_t 	speed: 2
uint32_t 	reserved: 28
 
Detailed Description
Structure of USB Port State.
```

### Enumerations
```
enum kdrv_usbh2_speed_t

Enumerations of USB Speed.

| Enumerator     									|
| USBH2_SPEED_LOW 	| Enum 0, USBH2 low speed		|
| USBH2_SPEED_FULL 	| Enum 1, USBH2 full speed		|
| USBH2_SPEED_HIGH 	| Enum 2, USBH2 high speed		|
```
```
enum kdrv_usbh2_port_event_t

Enumerations of USB Host Port Event.

| Enumerator     													|
| USBH2_EVENT_CONNECT 			| Enum 0x1, USBH2 connect event		|
| USBH2_EVENT_DISCONNECT 		| Enum 0x2, USBH2 disconect event	|
| USBH2_EVENT_OVERCURRENT 		| Enum 0x4, USBH2 overcurrent event	|
| USBH2_EVENT_RESET 			| Enum 0x8, USBH2 reset event		|
| USBH2_EVENT_SUSPEND 			| Enum 0x10, USBH2 suspend event	|
| USBH2_EVENT_RESUME 			| Enum 0x20, USBH2 resume event		|
| USBH2_EVENT_REMOTE_WAKEUP 	| Enum 0x40, USBH2 wakeup event		|
```
```
enum kdrv_usbh2_pipe_event_t

Enumerations of USB Host Pipe Event.

| Enumerator     															|
| USBH2_EVENT_TRANSFER_COMPLETE 	| Enum 0x1, Transfer completed			|
| USBH2_EVENT_HANDSHAKE_NAK 		| Enum 0x2, NAK Handshake received		|
| USBH2_EVENT_HANDSHAKE_NYET 		| Enum 0x4, NYET Handshake received		|
| USBH2_EVENT_HANDSHAKE_MDATA 		| Enum 0x8, MDATA Handshake receivedt	|
| USBH2_EVENT_HANDSHAKE_STALL 		| Enum 0x10, STALL Handshake received	|
| USBH2_EVENT_HANDSHAKE_ERR 		| Enum 0x20, ERR Handshake received		|
| USBH2_EVENT_BUS_ERROR 			| Enum 0x40, Bus Error detected			|
```
```
enum kdrv_usbh2_endpoint_type_t

Enumerations of USB Endpoint Type.

| Enumerator     															|
| USBH2_ENDPOINT_CONTROL 		| Enum 0, USBH2 endpoint control			|
| USBH2_ENDPOINT_ISOCHRONOUS 	| Enum 1, USBH2 endpoint irochrounous		|
| USBH2_ENDPOINT_BULK 			| Enum 2, USBH2 endpoint bulk				|
| USBH2_ENDPOINT_INTERRUPT 		| Enum 3, USBH2 endpoint interupt			|
```

### Functions
```
uint16_t kdrv_usbh2_get_frame_number	(	void 		)

USBH2 get frame number.

Parameters
	[in]	N/A	
Returns
	frame number
```
```
kdrv_status_t kdrv_usbh2_initialize	(	kdrv_usbh2_port_event_callback_t 	cb_port_event,
										kdrv_usbh2_pipe_event_callback_t 	cb_pipe_event 
									)		
USBH2 host mode driver initialization.

Parameters
	[in]	cb_port_event	see kdrv_usbh2_port_event_callback_t
	[in]	cb_pipe_event	see kdrv_usbh2_pipe_event_callback_t
Returns
	kdrv_status_t see kdrv_status_t
```
```

kdrv_usbh2_pipe_t kdrv_usbh2_pipe_create	(	uint8_t 	dev_addr,
												uint8_t 	dev_speed,
												uint8_t 	hub_addr,
												uint8_t 	hub_port,
												uint8_t 	ep_addr,
												uint8_t 	ep_type,
												uint16_t 	ep_max_packet_size,
												uint8_t 	ep_interval 
											)		
USBH2 create pipe.

Parameters
	[in]	dev_addr	device address
	[in]	dev_speed	device speed
	[in]	hub_addr	usb hub address
	[in]	hub_port	usb hub port
	[in]	ep_addr	endpoint address
	[in]	ep_type	endpoint type
	[in]	ep_max_packet_size	endpoint max packet size
	[in]	ep_interval	endpoint interval
Returns
	kdrv_usbh2_pipe_t see kdrv_usbh2_pipe_t
```
```
kdrv_status_t kdrv_usbh2_pipe_delete	(	kdrv_usbh2_pipe_t 	pipe_hndl	)

USBH2 pipe delete.

Parameters
	[in]	pipe_hndl	see kdrv_usbh2_pipe_t
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_usbh2_pipe_t kdrv_usbh2_pipe_isoch_create	(	uint8_t 	dev_addr,
													uint8_t 	ep_addr,
													uint16_t 	max_packet_size,
													uint8_t 	mult,
													uint8_t 	ep_interval,
													uint8_t * 	buf,
													uint32_t 	buf_size 
												)		
USBH2 pipe isoch create.

Parameters
	[in]	dev_addr	
	[in]	ep_addr	
	[in]	max_packet_size	
	[in]	mult	
	[in]	ep_interval	
	[in]	*buf	
	[in]	buf_size	
Returns
	kdrv_usbh2_pipe_t see kdrv_usbh2_pipe_t
```
```
kdrv_usbh2_isoch_itd_work_func_t kdrv_usbh2_pipe_isoch_enable_bh	(	kdrv_usbh2_pipe_t 	pipe_hndl,
																		kdrv_usbh2_isoch_bf_callback_t 	isoch_bf_callback 
																	)		
USBH2 pipe isoch transfer enable bh.

Parameters
	[in]	pipe_hndl	see kdrv_usbh2_pipe_t
	[in]	isoch_bf_callback	see kdrv_usbh2_isoch_bf_callback_t
Returns
	kdrv_usbh2_isoch_itd_work_func_t see kdrv_usbh2_isoch_itd_work_func_t
```
```
kdrv_status_t kdrv_usbh2_pipe_isoch_start	(	kdrv_usbh2_pipe_t 	pipe_hndl,
												kdrv_usbh2_isoch_data_callback_t 	isoch_data_cb 
											)		
USBH2 pipe isoch transfer start.

Parameters
	[in]	pipe_hndl	see kdrv_usbh2_pipe_t
	[in]	isoch_data_cb	see kdrv_usbh2_isoch_data_callback_t
Returns
	kdrv_status_t see kdrv_status_t
```
```
int32_t kdrv_usbh2_pipe_isoch_stop	(	kdrv_usbh2_pipe_t 	pipe_hndl	)	

USBH2 pipe isoch transfer stop.

Parameters
	[in]	pipe_hndl	see kdrv_usbh2_pipe_t
Returns
	KDRV_STATUS_OK
```
```
kdrv_status_t kdrv_usbh2_pipe_modify	(	kdrv_usbh2_pipe_t 	pipe_hndl,
											uint8_t 	dev_addr,
											uint8_t 	dev_speed,
											uint8_t 	hub_addr,
											uint8_t 	hub_port,
											uint16_t 	ep_max_packet_size 
										)		
USBH2 modify pipe.

Parameters
	[in]	pipe_hndl	see kdrv_usbh2_pipe_t
	[in]	dev_addr	device address
	[in]	dev_speed	device speed
	[in]	hub_addr	usb hub address
	[in]	hub_port	usb hub port
	[in]	ep_max_packet_size	endpoint max packet size
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbh2_pipe_reset	(	kdrv_usbh2_pipe_t 	pipe_hndl	)	

USBH2 pipe reset.

Parameters
	[in]	pipe_hndl	see kdrv_usbh2_pipe_t
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbh2_pipe_transfer	(	kdrv_usbh2_pipe_t 	pipe_hndl,
											kdrv_usbh2_packet_t 	packet,
											uint8_t * 	data,
											uint32_t 	num 
										)		
USBH2 pipe transfer.

Parameters
	[in]	pipe_hndl	see kdrv_usbh2_pipe_t
	[in]	packet	seew kdrv_usbh2_packet_t
	[in]	*data	Pointer to data buffer
	[in]	num	
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbh2_pipe_transfer_abort	(	kdrv_usbh2_pipe_t 	pipe_hndl	)	

USBH2 pipe transfer abort.

Parameters
	[in]	pipe_hndl	see kdrv_usbh2_pipe_t
Returns
	kdrv_status_t see kdrv_status_t
```
```
uint32_t kdrv_usbh2_pipe_transfer_get_result	(	kdrv_usbh2_pipe_t 	pipe_hndl	)

USBH2 pipe transfer get result.

Parameters
	[in]	pipe_hndl	see kdrv_usbh2_pipe_t
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_usbh2_port_state_t kdrv_usbh2_port_get_state	(	uint8_t 	port	)	

USBH2 get port state.

Parameters
	[in]	port	
Returns
	kdrv_usbh2_port_state_t see kdrv_usbh2_port_state_t
```
```
kdrv_status_t kdrv_usbh2_port_reset	(	uint8_t 	port	)

USBH2 port reset.

Parameters
	[in]	port	
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbh2_port_resume	(	uint8_t 	port	)	

USBH2 reset resume.

Parameters
	[in]	port	
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbh2_port_suspend	(	uint8_t 	port	)

USBH2 reset suspend.

Parameters
	[in]	port	
Returns
	kdrv_status_t see kdrv_status_t
```
```
kdrv_status_t kdrv_usbh2_uninitialize	(	void 		)
	
USBH2 host mode driver de-initialization.

Parameters
	[in]	N/A	
Returns
	kdrv_status_t see kdrv_status_t
```

## KDRV_WDT
Version

* v1.0

Copyright

* Copyright (C) 2020 Kneron, Inc. All rights reserved.

### Functions
```
typedef void(* wdt_interrupt_callback_t) (void *arg)

WDT user callback function. Note that this is callback form ISR context.
```
```
void kdrv_wdt_initialize	(	void 		)	

watchdog initialize for WDT IRQ setting.

Returns
	N/A
```
```
void kdrv_wdt_uninitialize	(	void 		)	

watchdog uninitialize for WDT IRQ setting.

Returns
	N/A
```
```
void kdrv_wdt_register_callback	(	wdt_interrupt_callback_t 	wdt_isr_cb,
									void * 	usr_arg 
								)		
set watchdog callback function.

Parameters
	[out]	wdt_isr_cb	callback function pointer
	[in]	usr_arg	parameter
```
```
void kdrv_wdt_enable	(	void 		)

watchdog enable

Returns
	N/A
```
```
void kdrv_wdt_disable	(	void 		)	

watchdog disable

Returns
	N/A
```
```
void kdrv_wdt_disable	(	void 		)

watchdog disable

Returns
	N/A
```
```
void kdrv_wdt_reset	(	void 		)	

watchdog reset, It will set protect key 0x5AB9 to trigger WDT system reset

Returns
	N/A
```
```
void kdrv_wdt_set_auto_reload	(	uint32_t 	value	)	

watchdog reload

Parameters
	[in]	value	watchdog reload value
Returns
	N/A
```
```
void kdrv_wdt_sys_int_enable	(	void 		)	

watchdog interrupt enable

Returns
	N/A
```
```
void kdrv_wdt_sys_int_disable	(	void 		)	

watchdog interrupt disable

Returns
	N/A
```
```
void kdrv_wdt_sys_reset_enable	(	void 		)	

watchdog reset enable

Returns
	N/A
```
```
void kdrv_wdt_sys_reset_disable	(	void 		)	

watchdog reset disable

Returns
	N/A
```
```
uint32_t kdrv_wdt_read_counter	(	void 		)	

watchdog read counter

Returns
	counter value
```
```
void kdrv_wdt_set_clear_status	(	void 		)	

watchdog status clear

Returns
	N/A
```
```
void kdrv_wdt_set_int_counter	(	uint8_t 	counter	)	

watchdog set interrupt counter

Parameters
	[in]	counter set the duration of assertion of wd_intr, the default value is 0xFF. which means that the default assertion duration is 256 clock cycles(PCLK)
Returns
	N/A
```
```
bool kdrv_wdt_is_counter_zero	(	void 		)	

watchdog, is counter zero

Returns
	bool
```
```
void kdrv_wdt_set_src_clock	(	uint8_t 	src_clk	)	

set watchdog source clock

Parameters
	[in]	src_clk	0: PCLK, 1:EXTCLK
Returns
	N/A
```
```
void kdrv_wdt_set_extclk_div	(	uint8_t 	val	)	

set watchdog external clock divider

Parameters
	[in]	val	external divider value, default:0x1D (max:0x1F)
Returns
	N/A
```
```
void kdrv_wdt_irq_enable	(	void 		)	

set watchdog irq enable

Returns
	N/A
```
```
void kdrv_wdt_irq_disable	(	void 		)	

set watchdog irq disable

Returns
	N/A
```
```
void kdrv_wdt_board_reset	(	uint32_t 	rst_cnt	)	

kdrv_wdt_board_reset, wdt board reset immediately.

Parameters
	[in]	rst_time	reset delay time (us)
Returns
	N/A
```
