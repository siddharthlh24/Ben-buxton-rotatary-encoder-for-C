# Ben-buxton-rotary-encoder-for-C
Super fast rotary encoder state machine with builtin debounce.<br>
This is a C port of the famous Ben Buxton's rotary encoder for Arduino. I did this with the original intent of using it with my STM32 blue pill.<br>
The original library is for Arduino and I had to strip out the consructor and make a few changes to make it work in C.<br>
Link to original Arduino library: https://github.com/buxtronix/arduino/tree/master/libraries/Rotary. Visit this for details. on the original library<br>

Demo video of my implementation:https://www.youtube.com/watch?v=Ni7hV8GAgFg <br>

The original function definition is changed to **unsigned char Pin_process(unsigned int _pin1,unsigned int  _pin2)** . This means the digital state of the encoder pins must be previously sampled and fed to the function. 

Half step output is **enabled** by default and can be disabled.

# Code snippet for reference
```
pinb5 = HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_5);   //digital read on STM32
pinb6 = HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_6);   //digital read on STM32

result = Pin_process(pinb5,pinb6);
if (result == DIR_CW) {
      count++;
      HAL_GPIO_TogglePin(GPIOC, GPIO_PIN_13);
    } else if (result == DIR_CCW) {
      --count;
      HAL_GPIO_TogglePin(GPIOC, GPIO_PIN_13);
    }
```
