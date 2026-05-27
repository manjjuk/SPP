# Campbell Shillinglaw Lau Ltd
## Speech Privacy Calculation Framework — Enclosed Office
**Version 1 (May 2026)**

---

### Reference Standard
*Salter, CM and Powell, K and Begault, D and Alvarado, R (2003) Case Studies of a Method for Predicting Speech Privacy in the Contemporary Workplace*

---

## 1. Acoustic Constraints & Reference Targets

### Voice Source Level ($L_{\\text{speech}}$)
* **Low:** Telephone conversation using a low voice level — **54 dBA**
* **Conversational:** Casual conversation in an office setting — **60 dBA** *(Default)*
* **Raised:** Conversation of three or more people in a meeting — **66 dBA**
* **Loud:** Talking into a speakerphone / presentation — **72 dBA**

### Speech Privacy Criteria ($C_{\\text{privacy}}$)
* **Confidential:** Audible but not intelligible — **15 dB** *(Default)*
* **Normal:** Audible and partially intelligible — **9 dB**
* **Marginal:** Speech from adjacent spaces is largely understandable — **3 dB**

### Continuous Background Noise Level ($L_{\\text{BG}}$)
* **Ambient Design Condition:** **35 dBA** *(Default, configurable range: 15 to 65 dBA)*

---

## 2. Boundary Room Profiles (Metric Inputs)

| Parameter | Default Value | Description / Options |
| :--- | :--- | :--- |
| **Source Room Floor Area** | `15.0 m²` | Minimum: $1\text{ m²}$ |
| **Source Room Material Finishes** | `Absorptive` | **Absorptive Surfaces:** $>50\%$ coverage (carpet, acoustic ceiling tiles)<br>**Hard Surfaces:** $<20\%$ coverage (drywall, concrete slab) |
| **Receive Room Floor Area** | `18.0 m²` | Minimum: $1\text{ m²}$ |
| **Receive Room Material Finishes** | `Absorptive` | **Absorptive Surfaces:** $>50\%$ coverage (soft furnishings, carpet)<br>**Hard Surfaces:** $<20\%$ coverage (glass facades, hard tiles) |
| **Shared Partition Wall Width** | `4.0 m` | Minimum: $0.5\text{ m}$ |
| **Shared Partition Wall Height** | `2.7 m` | Minimum: $0.5\text{ m}$ |

---

## 3. Calculation Framework & Methodology

The application dynamically calculates the minimum **Sound Transmission Class (STC)** or **Noise Isolation Class (NIC)** target using the following formula:

$$\\text{STC} = L_{\\text{speech}} + C_{\\text{privacy}} + \\Delta L_{\\text{source room}} - \\Delta L_{\\text{receiver room}} - L_{\\text{BG}} - \\text{Excess}$$

*Note: Excess is assumed to be `0` for an optimized privacy level without dissatisfaction. Input pairs can be evaluated as either STC/dBA or NIC/NC.*

### Underlying Matrix Functions

#### A. Source Room Correction Table ($\\Delta L_{\\text{source room}}$)
| Metric Floor Area ($A$) | Absorptive ($>50\%$) | Hard ($<20\%$) |
| :--- | :---: | :---: |
| $A > 93.03\text{ m²}$ | -3 dB | +3 dB |
| $46.52 < A \\le 93.03\text{ m²}$ | 0 dB | +6 dB |
| $23.26 < A \\le 46.52\text{ m²}$ | +3 dB | +9 dB |
| $11.63 < A \\le 23.26\text{ m²}$ | +6 dB | +12 dB |
| $A \\le 11.63\text{ m²}$ | +9 dB | +15 dB |

#### B. Receiver Room Correction Table ($\\Delta L_{\\text{receiver room}}$)
*Based on the ratio of the Receive Room Floor Area to the Shared Partition Wall Area ($A_{\\text{partition}} = \\text{Width} \\times \\text{Height}$).*

| Area / Wall Ratio | Absorptive ($>50\%$) | Hard ($<20\%$) |
| :--- | :---: | :---: |
| Ratio $\\ge 10.0$ | +10 dB | +5 dB |
| $6.0 \\le \\text{Ratio} < 10.0$ | +8 dB | +3 dB |
| $5.0 \\le \\text{Ratio} < 6.0$ | +7 dB | +2 dB |
| $4.0 \\le \\text{Ratio} < 5.0$ | +6 dB | +1 dB |
| $3.0 \\le \\text{Ratio} < 4.0$ | +5 dB | 0 dB |
| $2.0 \\le \\text{Ratio} < 3.0$ | +3 dB | -2 dB |
| $1.5 \\le \\text{Ratio} < 2.0$ | +2 dB | -3 dB |
| $1.0 \\le \\text{Ratio} < 1.5$ | 0 dB | -5 dB |
| $\\text{Ratio} < 1.0$ | 0 dB | -5 dB |

---

## 4. Speech Privacy Potential (SPP) Reference Matrix

$$\\text{Calculated SPP} = \\text{Final STC} + L_{\\text{BG}}$$

| Vocal Effort Classification | Source Amplitude Baseline | Required Equivalent SPP (Confidential) | Required Equivalent SPP (Normal) |
| :--- | :---: | :---: | :---: |
| **Low Voice** | 54 dBA | **70** | **65** |
| **Conversational Voice** | 60 dBA | **75** | **70** |
| **Raised Voice** | 66 dBA | **80** | **75** |
| **Loud Voice** | 72 dBA | **85** | **80** |
