![header](https://raw.githubusercontent.com/lyangmdrs/peripheral_interrupt_exercise/develop/Img/header.png?token=ADIW7OWNI4AYXAVKGCOPQ2DAGUNFA)
***
# Peripheral Interruption

The goal of this exercise is to pend a USART3 interrupt and the implement the **Interrupt Service Routine** (**ISR**).

### Interrupt Set-pending Register (ISPR)

Firstly we need to discover wich bit of ISPR is responsable for indicate a pending interruption from USART3.  From the [STM32F4xxx - Reference Manual 0090](https://github.com/lyangmdrs/peripheral_interrupt_exercise/blob/develop/Docs/STM32F4xxx_-_RM0090.pdf), on table 61, we can extract the information that it's the bit 39 from ISRP. But, on the table 4-2 from [Generic User Guide](https://github.com/lyangmdrs/peripheral_interrupt_exercise/blob/develop/Docs/Cortex-M4_Devices_-_Generic_User_Guide.pdf), we can see that exists at all 8 registers composing the ISPR, each one with 32 bits, named from NVIC_ISPR0 to NVIC_ISPR7. On the NVIC_ISPR0 are located the bits 0 to 31. Thus, in the NVIC_ISPR1 are located the next 32 bits, starting from 32 to 63, and this logic continues for the remaining registers. Therefore, the bit 39 of ISPR is mapped to the bit 7 of NVIC_ISPR1. On the [code](https://github.com/lyangmdrs/peripheral_interrupt_exercise/blob/83918f4f3ba2beb232ce3b63ca3452c555cb8558/Src/main.c#L35) was used the Modulus Operator (**%**) to calculate position of the bit 39 of ISPR on NVIC_ISPR1 register. 

It's important to know that, in a real scenario, the peripehals are responsable to pend their interruptions. So the 34th and 35th lines from [main.c](https://github.com/lyangmdrs/peripheral_interrupt_exercise/blob/develop/Src/main.c) would not be needed.

In the following lines, the interruption is porperly enabled, and as result, the ISR function for USART3 will be executed. The name for all ISR functions are predefined on [startup_stm32f407vetx.s](https://github.com/lyangmdrs/peripheral_interrupt_exercise/blob/83918f4f3ba2beb232ce3b63ca3452c555cb8558/Startup/startup_stm32f407vetx.s#L186) file.



> Exercise from [**Embedded Systems Programming on ARM Cortex-M3/M4 Processor**](https://www.udemy.com/course/embedded-system-programming-on-arm-cortex-m3m4/)

***
