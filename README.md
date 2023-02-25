# STM32F427GPIOTEST


## Developer's Tools

The project for STM32CubeIDE 1.11.2

For the arch based linux can be installed

```
yay stm32cubeide
```


To change the JTAG Programmer:

1. Use the mainmenu option "/Run/Run Configurations..."
2. Then, at the left item's tree select "/Stm32C/C++ Application//STM32F427GPIOTESTX Debug" 
3. Then, at the right side of the three select a "Debug" tab 
4. With "Debug" tab active change a "Debug Probe" to yours (aka JLink or STLink)


## Main Loop

The main /task/ code in the body of /StartDefaultTask/ function at the end of *Core/Src/main.c* file;

```
void StartDefaultTask(void *argument)
{
  /* USER CODE BEGIN 5 */
  /* Infinite loop */
  for(;;)
  {
	/* A BABY TALK */

	// Read the inputs
	GPIO_PinState gf6 = HAL_GPIO_ReadPin(GPIOF, GPIO_PIN_6);
	GPIO_PinState gf7 = HAL_GPIO_ReadPin(GPIOF, GPIO_PIN_7);
	GPIO_PinState gf8 = HAL_GPIO_ReadPin(GPIOF, GPIO_PIN_8);
	GPIO_PinState gf9 = HAL_GPIO_ReadPin(GPIOF, GPIO_PIN_9);

	// GPIO_PinState has 0 or 1 integer value, so then can be used bitwise and
	// it is less portable but good enough for test
	GPIO_PinState gf10 = (int)gf6 & (int)gf7;
	GPIO_PinState gf11 = (int)gf8 & (int)gf9;

	// Write the outputs
	HAL_GPIO_WritePin(GPIOF, GPIO_PIN_0, gf6);
	HAL_GPIO_WritePin(GPIOF, GPIO_PIN_1, gf7);
	HAL_GPIO_WritePin(GPIOF, GPIO_PIN_2, gf8);
	HAL_GPIO_WritePin(GPIOF, GPIO_PIN_3, gf9);
	HAL_GPIO_WritePin(GPIOF, GPIO_PIN_10, gf10);
	HAL_GPIO_WritePin(GPIOF, GPIO_PIN_11, gf11);

    osDelay(10);
  }
  /* USER CODE END 5 */
}
```
