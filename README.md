# Signal Resilience Sim: Channel Coding for Video over a Noisy Channel

MATLAB simulation of sending raw video frames over a binary symmetric channel (BSC) with a punctured convolutional code. It compares a fixed rate-1/2 code with an incremental-redundancy scheme that starts at a high code rate and falls back to lower rates when a packet is not decoded correctly.

## What it does

- Reads an RGB video (`highway.avi` / `foreman.avi`, 144 x 176 frames), converts each colour channel to bits (608,256 bits per frame) and splits them into 1,024-bit packets.
- Encodes each packet with a rate-1/2 convolutional code, constraint length 7, generators [171 133] octal (`poly2trellis`, `convenc`).
- Punctures the code to rates 8/9, 4/5, 2/3, 4/7 and 1/2.
- Passes the coded bits through a BSC (`bsc`) and decodes with a hard-decision Viterbi decoder, traceback depth 35 (`vitdec`).
- **Incremental redundancy:** each packet is first sent at rate 8/9; if the decoded packet differs from the original, it is re-sent at the next lower rate (4/5, 2/3, 4/7, then 1/2).
- `Code.m` applies incremental redundancy to every frame at error probability p = 0.01 and writes the received video to `NewVideoFile.avi`.
- The plotting scripts sweep p from 0.0001 to 0.19 (step 0.01) on the first frame and plot:
  - BER vs. p for the fixed rate-1/2 code
  - BER vs. p for incremental redundancy
  - transmitted bits per frame divided by information bits (labelled "Throughput" in the plot) vs. p for incremental redundancy

## Tech stack

MATLAB (screenshots show R2020b) with the Communications Toolbox (`convenc`, `vitdec`, `poly2trellis`, `bsc`, `de2bi`, `bi2de`).

## Repository contents

| Path | Description |
|------|-------------|
| `Code.m` | Full video transmission with incremental redundancy at p = 0.01; writes and plays the received video |
| `Screenshots/Codes of the screenshots/HalfCodePlot.m` | BER vs. p for the fixed rate-1/2 code |
| `Screenshots/Codes of the screenshots/IncrementalRedundancyBER.m` | BER vs. p for incremental redundancy |
| `Screenshots/Codes of the screenshots/IncrementalRedundancyThruput.m` | Transmitted / information bit ratio vs. p for incremental redundancy |
| `Screenshots/*.png` | MATLAB screenshots of the three plots |
| `Videos/*.avi` | Received videos for no channel coding (`NoChannelCoding*`), rate-1/2 coding (`CodeHalf*`) and incremental redundancy (`IncrementalCode*`), at two error settings (file suffixes `001` and `1`) |

The input videos (`highway.avi`, `foreman.avi`) and the script for the uncoded case are not included in the repository.

## Results

From the screenshots (values read off the plots, so approximate):

- With both the fixed rate-1/2 code and incremental redundancy, BER is close to zero for small p and rises to about 0.45 at p = 0.19.
- With incremental redundancy, the ratio of transmitted to information bits starts at about 1.1 (most packets succeed at rate 8/9) and reaches 2, i.e. every packet needs the rate-1/2 code, from about p = 0.06.

**BER vs. p, rate-1/2 code**

![BER vs p for rate 1/2](Screenshots/Half%20Code%20Plot%20Screenshot.png)

**BER vs. p, incremental redundancy**

![BER vs p for incremental redundancy](Screenshots/Incremental%20Redundancy%20BER%20plot.png)

**Transmitted / information bits vs. p, incremental redundancy**

![Throughput vs p for incremental redundancy](Screenshots/Incremental%20Redundancy%20Throughput%20plot.png)

## How to run

1. Install MATLAB with the Communications Toolbox.
2. Put a 144 x 176 RGB video named `highway.avi` (for `Code.m` and `HalfCodePlot.m`) or `foreman.avi` (for the incremental-redundancy scripts) in the working folder. These are standard QCIF test sequences.
3. Run `Code.m` to produce `NewVideoFile.avi`, or run one of the scripts in `Screenshots/Codes of the screenshots/` to produce a plot.

---
*Developed by Khaled Walid*
