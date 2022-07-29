# Juxta
 
__TI CCS Dev__

> Use LP_CC1352P7_4 projects for your CC2652P7 device.  This is also covered in the Running Software Examples on CC2652P module of the BLE5-Stack Migration Guide.  You still need an antenna switch to determine whether to use the normal or high-PA output path, although if using a custom design with one determined path then you can choose "Use Custom Board" and remove the CONFIG_RF_* pin assignments.

* In CCS > *.syscfg click the Board icon, select "Use custom board"
* Make a new target file for CC2652P7 and right-click it active

${COM_TI_SIMPLELINK_CC13XX_CC26XX_SDK_INSTALL_DIR_REPOS}

__Base SysConfig (no RF)__

		/**
	 * These arguments were used when this file was generated. They will be automatically applied on subsequent loads
	 * via the GUI or CLI. Run CLI with '--help' for additional information on how to override these arguments.
	 * @cliArgs --device "CC1352P7RGZ" --package "RGZ" --part "Default" --rtos "tirtos7" --product "simplelink_cc13xx_cc26xx_sdk@6.10.00.29"
	 * @versions {"tool":"1.12.0+2406"}
	 */
	
	/**
	 * Import the modules used in this configuration.
	 */
	const rfdesign    = scripting.addModule("/ti/devices/radioconfig/rfdesign");
	const ADC         = scripting.addModule("/ti/drivers/ADC", {}, false);
	const ADC1        = ADC.addInstance();
	const GPIO        = scripting.addModule("/ti/drivers/GPIO");
	const GPIO2       = GPIO.addInstance();
	const GPIO3       = GPIO.addInstance();
	const GPIO4       = GPIO.addInstance();
	const GPIO5       = GPIO.addInstance();
	const GPIO6       = GPIO.addInstance();
	const GPIO7       = GPIO.addInstance();
	const GPIO8       = GPIO.addInstance();
	const Power       = scripting.addModule("/ti/drivers/Power");
	const SPI         = scripting.addModule("/ti/drivers/SPI", {}, false);
	const SPI1        = SPI.addInstance();
	const Settings    = scripting.addModule("/ti/posix/tirtos/Settings");
	const BIOS        = scripting.addModule("/ti/sysbios/BIOS");
	const Event       = scripting.addModule("/ti/sysbios/knl/Event");
	const Idle        = scripting.addModule("/ti/sysbios/knl/Idle", {}, false);
	const Idle2       = Idle.addInstance();
	const Mailbox     = scripting.addModule("/ti/sysbios/knl/Mailbox");
	const Error       = scripting.addModule("/ti/sysbios/runtime/Error");
	const SysCallback = scripting.addModule("/ti/sysbios/runtime/SysCallback");
	const Timestamp   = scripting.addModule("/ti/sysbios/runtime/Timestamp");
	
	/**
	 * Write custom configuration values to the imported modules.
	 */
	rfdesign.fbSub1g = "none";
	rfdesign.fe24g   = "ID";
	rfdesign.pa20    = "none";
	
	ADC1.$name              = "VBATT";
	ADC1.adc.adcPin.$assign = "DIO_27";
	
	GPIO2.$name           = "LED_1";
	GPIO2.mode            = "Output";
	GPIO2.outputStrength  = "Low";
	GPIO2.gpioPin.$assign = "DIO_6";
	
	GPIO3.$name              = "AXY_CS";
	GPIO3.mode               = "Output";
	GPIO3.initialOutputState = "High";
	GPIO3.gpioPin.$assign    = "DIO_16";
	
	GPIO4.$name           = "AXY_INT";
	GPIO4.pull            = "Pull Up";
	GPIO4.gpioPin.$assign = "DIO_17";
	
	GPIO5.$name           = "DEBUG";
	GPIO5.gpioPin.$assign = "DIO_22";
	
	GPIO6.$name           = "Rx";
	GPIO6.gpioPin.$assign = "DIO_24";
	
	GPIO7.$name           = "Tx";
	GPIO7.mode            = "Output";
	GPIO7.gpioPin.$assign = "DIO_25";
	
	GPIO8.$name           = "LED_0";
	GPIO8.mode            = "Output";
	GPIO8.outputStrength  = "Low";
	GPIO8.gpioPin.$assign = "DIO_26";
	
	const CCFG              = scripting.addModule("/ti/devices/CCFG", {}, false);
	CCFG.ccfgTemplate.$name = "ti_devices_CCFG_CCFGCC26XXTemplate0";
	
	SPI1.$name               = "CONFIG_SPI";
	SPI1.spi.sclkPin.$assign = "DIO_19";
	SPI1.spi.misoPin.$assign = "DIO_20";
	SPI1.spi.mosiPin.$assign = "DIO_21";
	
	BIOS.assertsEnabled = false;
	BIOS.heapBaseAddr   = "__primary_heap_start__";
	BIOS.heapEndAddr    = "__primary_heap_end__";
	
	const Hwi           = scripting.addModule("/ti/sysbios/family/arm/m3/Hwi", {}, false);
	Hwi.enableException = false;
	
	const Clock      = scripting.addModule("/ti/sysbios/knl/Clock", {}, false);
	Clock.tickPeriod = 10;
	
	const Timer       = scripting.addModule("/ti/sysbios/family/arm/cc26xx/Timer", {}, false);
	Timer.rtc.$assign = "RTC0";
	
	Idle2.$name   = "powerIdle";
	Idle2.idleFxn = "Power_idleFunc";
	
	const Semaphore            = scripting.addModule("/ti/sysbios/knl/Semaphore", {}, false);
	Semaphore.supportsPriority = false;
	
	const Swi         = scripting.addModule("/ti/sysbios/knl/Swi", {}, false);
	Swi.numPriorities = 6;
	
	const Task             = scripting.addModule("/ti/sysbios/knl/Task", {}, false);
	Task.defaultStackSize  = 512;
	Task.idleTaskStackSize = 512;
	Task.numPriorities     = 6;
	
	Error.policy       = "Error_SPIN";
	Error.printDetails = false;
	
	const System           = scripting.addModule("/ti/sysbios/runtime/System", {}, false);
	System.abortFxn        = "System_abortSpin";
	System.exitFxn         = "System_exitSpin";
	System.extendedFormats = "%f";
	System.supportModule   = "SysCallback";
	
	/**
	 * Pinmux solution for unlocked pins/peripherals. This ensures that minor changes to the automatic solver in a future
	 * version of the tool will not impact the pinmux you originally saw.  These lines can be completely deleted in order to
	 * re-solve from scratch.
	 */
	ADC1.adc.$suggestSolution              = "ADC0";
	SPI1.spi.$suggestSolution              = "SSI0";
	SPI1.spi.dmaRxChannel.$suggestSolution = "DMA_CH3";
	SPI1.spi.dmaTxChannel.$suggestSolution = "DMA_CH4";


