# Benchmarks

Phone: Galaxy S26 (Exynos 2600: 1x C1-Ultra 3.8 GHz, 3x C1-Pro 3.25 GHz, 6x C1-Pro 2.75 GHz; Xclipse 960 GPU, 12 GB).
Software: Termux, llama.cpp 0.7.0 with the Vulkan backend, Samsung GPU driver 25.3.21.

## Results (GPU only, `-ngl 99`)

| Model | Threads | pp512 | Generation |
| --- | --- | --- | --- |
| Llama 3.2 3B | 2 | 312.9 t/s | 28.9 t/s (tg128) |
| Qwen3 4B | 2 | 232.0 t/s | 23.2 t/s (tg32) |
| Qwen3 4B | 4 | 230.8 t/s | 21.8 t/s (tg32) |

## Findings

- **Flash attention is slower on this GPU** (Qwen3.5-4B: 213 → 168 t/s prompt). Use `-fa 0`.
- **Skin temperature is the limit.** The GPU runs at its full 980 MHz until the phone's skin reaches 45 °C, then is capped (836–874 MHz, and as low as 408–557 MHz in long runs). Android's thermal status stays at 0; the cap comes from Samsung's thermal management.
- **Power draw** peaks around 11.6 W for the whole phone at full GPU clock, and settles at 5–6 W once capped.
- **More CPU threads do not help** when the model is fully on the GPU: 2–3 threads on the performance cores are best.

## Monitoring without root

A small script reads clocks and loads from sysfs, live temperatures from `dumpsys thermalservice` (the "Current temperatures from HAL" list, not the cached one), GPU temperature from `/sys/kernel/gpu/gpu_tmu`, and battery current and voltage from `dumpsys battery`, all over local adb.
