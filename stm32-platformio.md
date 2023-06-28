## stm32cubemx platformio 配置文件


### `正点原子mini v4`
```
[platformio]
src_dir = ./
include_dir = Core/Inc
[env:genericSTM32F103RC]
platform = ststm32
board = genericSTM32F103RC
build_flags = 
	-D STM32F103xx
	-ICore/Inc
	-IDrivers/CMSIS/Include
	-IDrivers/CMSIS/Device/ST/STM32F1xx/Include
	-IDrivers/STM32F1xx_HAL_Driver/Inc
	-IDrivers/STM32F1xx_HAL_Driver/Inc/Legacy
src_filter = +<Core/Src> +<startup_stm32f103xe.s> +<Drivers/> +<Middlewares/>
board_build.ldscript = ./STM32F103RCTx_FLASH.ld
upload_protocol = serial
monitor_speed = 115200
```

### DIY `F103C8T6`
```
[env:genericSTM32F103C8]
platform = ststm32
board = genericSTM32F103C8
; framework = stm32cube
build_flags = 
	-D STM32F103xx
	-ICore/Inc
	-IDrivers/CMSIS/Include
	-IDrivers/CMSIS/Device/ST/STM32F1xx/Include
	-IDrivers/STM32F1xx_HAL_Driver/Inc
	-IDrivers/STM32F1xx_HAL_Driver/Inc/Legacy
src_filter = +<Core/Src> +<startup_stm32f103xb.s> +<Drivers/> +<Middlewares/>
board_build.ldscript = ./STM32F103C8Tx_FLASH.ld
upload_protocol = stlink 
debug_tool = stlink






[platformio]
src_dir = ./
include_dir = Core/Inc
```

