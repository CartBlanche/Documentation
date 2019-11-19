---
uid: Meadow.Foundation.Displays.Tft.ILI9341
remarks: *content
---

### Purchasing

You can get ILI9341 displays from the following suppliers:

* [AliExpress]()
* [Ebay]()
* [Amazon]()

### Code Example

The following example shows how to initialize a ILI9341 display and draw three lines using `DrawPixel` method:

```csharp
using System;
using System.Threading;
using Meadow;
using Meadow.Devices;
using Meadow.Foundation.Displays.Tft;
using Meadow.Hardware;

namespace ILI9341_Sample
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
        protected ILI9341 ILI9341;

        public MeadowApp ()
        {
            spiBus = Device.CreateSpiBus();

            ILI9341 = new ILI9341(
                device: Device, 
                spiBus: spiBus,
                chipSelectPin: null,
                dcPin: Device.Pins.D01,
                resetPin: Device.Pins.D00,
                width: 240, height: 240);

            Console.WriteLine("Clear display");
            ILI9341.ClearScreen(250);
            ILI9341.Refresh();

            Console.WriteLine("Draw lines");
            for (int i = 0; i < 30; i++)
            {
                ILI9341.DrawPixel(i, i, true);
                ILI9341.DrawPixel(30 + i, i, true);
                ILI9341.DrawPixel(60 + i, i, true);
            }

            ILI9341.Show(); 
        }
    }
}
```

### Circuit Example

 To wire a ILI9341 to your Meadow board, connect the following:

| ILI9341  | Meadow Pin |
|---------|------------|
| GND     | GND        |
| VCC     | 3V3        |
| SCL     | SCK        |
| SDA     | MOSI       |
| RESET   | D00        |
| DC      | D01        |

It should look like the following diagram:

![](../../API_Assets/Meadow.Foundation.Displays.Tft.ILI9341/ILI9341_Fritzing.png)