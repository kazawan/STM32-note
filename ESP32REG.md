### ☣️操作寄存器

`参考地址`
[WOKWI ESP32 寄存器操作](https://wokwi.com/projects/368567923857784833)

寄存器地址 0 - 31  32-36有另外的方法
```
#define PARALLEL_0  24 //从24开始

int value ;
void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
  Serial.println("Hello, ESP32!");
  REG_WRITE(GPIO_ENABLE_W1TS_REG, 0x6 << PARALLEL_0); // 0x6 = 0110
  
}

void loop() {
  // put your main code here, to run repeatedly:
  value = 0x02; // 0x02 = 0010 25号管脚打开 26号关闭
  REG_WRITE(GPIO_OUT_REG, value << PARALLEL_0); 
  delay(200); // this speeds up the simulation
  value = 0x04 ; //0x04 = 0100 25号管脚关闭 26号打开
  REG_WRITE(GPIO_OUT_REG, value << PARALLEL_0);
  delay(200); // this speeds up the simulation
}
```




