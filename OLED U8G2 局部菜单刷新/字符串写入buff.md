
# 基于u8g2 写入字符串
## 写入单个字符

```c
/**
 * @brief 写单一个字符
 * @param x 字符起始x坐标
 * @param y 字符起始y坐标
 * @param str 字符
 * @param exte_font 字体
 * @param margin 字符间距
*/
void writeChar(int x, int y, char str,custom_font_t *exte_font = exte_font_10x12)
{
  int str_offset = 65;//0开始的偏移量
  int str_index = str - str_offset; // 字符在数组中的索引

  
  uint8_t w = exte_font[str_index].width;
  uint8_t h = exte_font[str_index].height;
  uint8_t *data = exte_font[str_index].data;
  uint8_t i;
  uint8_t j;
  uint8_t k;
  uint8_t temp1;
  uint8_t temp2;
  uint8_t t1 = 8;
  // uint8_t margin = 2;
  for (i = 0; i < w; i++)
  {
    uint8_t index = 2 * i ;
    uint16_t temp = (data[index+1] << 8 | data[index]);    // 缓存当前图片+偏移量
    temp1 = temp & 0xff;                          // 取低8位
    temp2 = temp >> 8 & 0xff;                     // 取高8位
    for (j = 0; j < t1; j++)                      // 画低8位
    {
      if (temp1 >> j & 0x01)
      {
        u8g2.drawPixel(x + i, y + j);
      }
    }
    {
      if (temp1 >> j & 0x01)
      {
        u8g2.drawPixel(x + i, y + j);
      }
    }
    for (k = 0; k < h - 8; k++) // 画高8位
    {
      if (temp2 >> k & 0x01)
      {
        u8g2.drawPixel(x + i, y + k + 8);
      }
    }
  }
}
```

## 写入字符串

```c
/**
 * @brief 写字符串
 * @param x 字符串起始x坐标
 * @param y 字符串起始y坐标
 * @param ch 字符串
 * @param str_len 字符串长度
 * @param exte_font 字体
 * @param margin 字符间距
*/
void writeString(int x, int y, u8 ch[],uint8_t str_len,custom_font_t *exte_font = exte_font_10x12,int margin = 1)
{
  uint8_t i;
  uint8_t font_w = exte_font[0].width;
  uint8_t font_w_margin = font_w + margin;
  for(i = 0 ; i < str_len ; i++)
  {
    // int ascii_value = (int) ch[i];
    writeChar(x + i*font_w_margin  , y, ch[i],exte_font);
  }
  
  
}
```

## 使用

```c
    u8g2.clearBuffer();
    char msg[] = "ABCD";
    writeString(10,10,(uint8_t*)msg,4,exte_font_10x12_2);
    u8g2.drawBox(0, 0, 8, 8);
    u8g2.sendBuffer();
```