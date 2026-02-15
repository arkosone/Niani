# Simulation 002 - Material Comparison

**Date:** February 15, 2026  
**Tool:** MEEP  
**Objective:** Compare light confinement in different materials (glass, polymer, silicon)

---

## Hypothesis

Different materials (different ε) will show:
1. Different confinement strength
2. Different number of oscillations (wavelength change)
3. Different evanescent field extent

**Prediction:** Silicon (highest ε) will have strongest confinement and most oscillations.

---

## Setup

### Three Materials Tested

**Glass:**
- ε = 2.25
- n = √2.25 = 1.5
- Common optical material (fiber optics)

**Polymer:**
- ε = 2.5
- n = √2.5 ≈ 1.58
- Plastic optical materials

**Silicon:**
- ε = 12
- n = √12 ≈ 3.46
- Standard for integrated photonics

### Simulation Parameters
- **Same for all:** Cell size, source, resolution
- **Only difference:** Material permittivity (ε)

---

## Results

### Visual Comparison

**Observed patterns (left to right: Glass, Polymer, Silicon):**

**Glass (ε=2.25):**
- ~5-6 oscillations visible
- Significant evanescent field (light extends into air)
- Weak confinement

**Polymer (ε=2.5):**
- ~5-6 oscillations (similar to glass)
- Evanescent field still significant
- Slightly better confinement than glass

**Silicon (ε=12):**
- ~10-12 oscillations (2× more)
- Minimal evanescent field
- Strong confinement

---

## Analysis

### Key Findings

**1. Refractive index determines wavelength in material:**
```
λ_material = λ_vacuum / n

Glass (n=1.5):    λ_glass = λ₀ / 1.5  ≈ 0.67 λ₀
Polymer (n=1.58): λ_poly = λ₀ / 1.58 ≈ 0.63 λ₀
Silicon (n=3.46): λ_Si = λ₀ / 3.46   ≈ 0.29 λ₀
```

**Shorter wavelength = More oscillations in same space**

**This matches observations:** Si has ~2× more oscillations than glass.

---

**2. Index contrast determines confinement:**
```
Air/Glass interface:    n_contrast = 1.5 / 1.0  = 1.5×
Air/Polymer interface:  n_contrast = 1.58 / 1.0 = 1.58×
Air/Silicon interface:  n_contrast = 3.46 / 1.0 = 3.46×
```

**Higher contrast = Stronger confinement**

**Si confines much better than glass/polymer.**

---

**3. Small ε differences (glass vs polymer) have small effects:**

Glass (ε=2.25) and Polymer (ε=2.5) behave very similarly:
- Both ~5-6 oscillations
- Both weak confinement
- Difficult to distinguish visually

**Silicon (ε=12) is dramatically different.**

---

## Implications for NIANI

### Material Choice is Critical

**For dense photonic circuits (NIANI goal):**

✅ **Silicon (or similar high-n material) is optimal:**
- Strong confinement → Waveguides can be placed close together
- Tight bending → Compact circuits possible
- Miniaturization → Millions of neurons on small chip

❌ **Glass/Polymer insufficient:**
- Weak confinement → Requires large spacing
- Loose bending → Large circuits
- Cannot achieve density needed for brain-like architecture

### But Trade-offs Exist

**Silicon challenges:**
- Expensive fabrication (cleanroom)
- Opaque in visible (only works in IR >1100nm)
- Complex processing

**Polymer advantages:**
- Cheap, easy to make
- Visible transparency
- Flexible

**For NIANI v0.1 (prototype):** Silicon is necessary despite cost.

**For NIANI v1.0+ (product):** May need new materials (high-n + visible transparency).

---

## What I Learned

### Physics Confirmed Experimentally

**Before:** I read that n = √ε and λ = λ₀/n

**After:** I SAW it in simulation. Theory → Reality.

This reinforces that:
- Physics equations are not arbitrary
- They describe real, observable phenomena
- Simulation can validate understanding

### Intuition Developed

Now I can "feel" what different ε values mean:
- ε = 2-3: Weak confinement, large circuits
- ε = 10-15: Strong confinement, dense circuits

This intuition will guide future design choices.

---

## Next Steps

- [ ] Test intermediate materials (Si₃N₄, ε ≈ 5.76)
- [ ] Simulate losses (absorption coefficient)
- [ ] Test curved waveguides (bending radius vs material)
- [ ] Multi-layer structures (Si on SiO₂ substrate)

---

## Code

See `notebook.ipynb` for complete comparison code.

**Key modification:**
```python
def simulate_material(epsilon, material_name):
    geometry = [
        mp.Block(
            size=mp.Vector3(mp.inf, 1, mp.inf),
            material=mp.Medium(epsilon=epsilon)  # Variable
        )
    ]
    # ... rest of simulation
    return field_data

# Run for each material
ez_glass = simulate_material(2.25, "Glass")
ez_polymer = simulate_material(2.5, "Polymer")
ez_silicon = simulate_material(12.0, "Silicon")

# Plot side-by-side comparison
```

---

## Images

*(Upload your 3-panel comparison image here)*

---

## Notes

**Personal insight:**

This simulation taught me that **material choice is not just a detail - it's 
fundamental to architecture possibilities.**

For NIANI, we can't just pick "any material that guides light." We need materials 
with specific properties (high-n, reconfigurable, low-loss) to achieve the vision.

This is why the "miracle material" search (docs/ideal-material.md) is so critical. 
Without the right material, NIANI remains theoretical.

**But:** Even with imperfect materials (like current PCMs), we can build functional 
prototypes. Perfect is not required for progress.

---

*Simulation 002 - Understanding material fundamentals.*
