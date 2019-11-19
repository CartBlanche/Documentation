---
uid: Meadow.Foundation.Displays.Tft.SSD1351
remarks: *content
---

### Purchasing

You can get SSD1351 displays from the following suppliers:

* [AliExpress]()
* [Ebay]()
* [Amazon]()

### Code Example

The following example shows how to initialize a SSD1351 display and draw three lines using `DrawPixel` method:

```csharp
using System;
using System.Threading;
using Meadow;
using Meadow.Devices;
using Meadow.Foundation.Displays.Tft;
using Meadow.Hardware;

namespace SSD1351_Sample
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
        protected SSD1351 SSD1351;

        public MeadowApp ()
        {
            spiBus = Device.CreateSpiBus();

            SSD1351 = new SSD1351(
                device: Device, 
                spiBus: spiBus,
                chipSelectPin: null,
                dcPin: Device.Pins.D01,
                resetPin: Device.Pins.D00,
                width: 240, height: 240);

            Console.WriteLine("Clear display");
            SSD1351.ClearScreen(250);
            SSD1351.Refresh();

            Console.WriteLine("Draw lines");
            for (int i = 0; i < 30; i++)
            {
                SSD1351.DrawPixel(i, i, true);
                SSD1351.DrawPixel(30 + i, i, true);
                SSD1351.DrawPixel(60 + i, i, true);
            }

            SSD1351.Show(); 
        }
    }
}
```

### Circuit Example

 To wire a SSD1351 to your Meadow board, connect the following:

| SSD1351  | Meadow Pin |
|---------|------------|
| GND     | GND        |
| VCC     | 3V3        |
| SCL     | SCK        |
| SDA     | MOSI       |
| RESET   | D00        |
| DC      | D01        |

It should look like the following diagram:

![](../../API_Assets/Meadow.Foundation.Displays.Tft.SSD1351/SSD1351_Fritzing.png)