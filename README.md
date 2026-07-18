# focus dashboard
A compact desk device with three circular TFT displays that shows the information I was constantly unlocking my phone to check — the current time, a Pomodoro focus timer, and my next calendar event. The goal was an always-on ambient display that communicates in peripheral vision without demanding attention.
Built around three GC9A01 1.28" round colour displays driven by an ESP32 WROVER, with a custom multi-part enclosure designed in OnShape and 3D printed from scratch. The firmware uses LovyanGFX with sprite-based DMA rendering to drive all three displays off a shared SPI bus simultaneously. The calendar display syncs live with Google Calendar over WiFi. This is an incoming first-year mechatronics engineering project built over the summer before university — documented here as it's built.

<img width="2880" height="2160" alt="fdc" src="https://github.com/user-attachments/assets/b345b714-04bf-4892-a09c-7a356c25ca59" />
# initial parts list

