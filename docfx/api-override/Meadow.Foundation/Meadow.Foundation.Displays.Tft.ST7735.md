---
uid: Meadow.Foundation.Displays.Tft.ST7735
remarks: *content
---

### Purchasing

You can get ST7735 displays from the following suppliers:

* [AliExpress]()
* [Ebay]()
* [Amazon]()

### Code Example

The following example shows how to initialize a ST7735 display and draw three lines using `DrawPixel` method:

```csharp
using System;
using System.Threading;
using Meadow;
using Meadow.Devices;
using Meadow.Foundation.Displays.Tft;
using Meadow.Hardware;

namespace ST7735_Sample
{
    public class Program
    {
        static IApp _app; 
        public static void Main()
        {
            _app = new MeadowApp();
        }
    }
    
    public class MeadowApp : AppBase<F7Micro, App>
    {
        protected ISpiBus spiBus;
        protected ST7735 ST7735;

        public MeadowApp ()
        {
            spiBus = Device.CreateSpiBus();

            ST7735 = new ST7735(
                device: Device, 
                spiBus: spiBus,
                chipSelectPin: null,
                dcPin: Device.Pins.D01,
                resetPin: Device.Pins.D00,
                width: 240, height: 240);

            Console.WriteLine("Clear display");
            ST7735.ClearScreen(250);
            ST7735.Refresh();

            Console.WriteLine("Draw lines");
            for (int i = 0; i < 30; i++)
            {
                ST7735.DrawPixel(i, i, true);
                ST7735.DrawPixel(30 + i, i, true);
                ST7735.DrawPixel(60 + i, i, true);
            }

            ST7735.Show(); 
        }
    }
}
```

### Circuit Example

 To wire a ST7735 to your Meadow board, connect the following:

| ST7735  | Meadow Pin |
|---------|------------|
| GND     | GND        |
| VCC     | 3V3        |
| SCL     | SCK        |
| SDA     | MOSI       |
| RESET   | D00        |
| DC      | D01        |

It should look like the following diagram:

![](../../API_Assets/Meadow.Foundation.Displays.Tft.ST7735/ST7735_Fritzing.png)