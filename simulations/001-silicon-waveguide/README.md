# Simulation 001 - Silicon Waveguide

**Date:** February 15, 2026  
**Tool:** MEEP (MIT Electromagnetic Equation Propagation)  
**Objective:** First photonic simulation - understand light propagation in silicon waveguide

---

## Setup

### Geometry
- **Cell size:** 20 × 6 units (2D)
- **Waveguide:** Silicon strip (ε = 12, n ≈ 3.46)
  - Width: 1 unit
  - Length: Infinite (spans entire cell)
  - Position: Centered vertically
- **Cladding:** Air (ε = 1)
- **Boundary:** PML (Perfectly Matched Layer, 1 unit thick)

### Source
- **Type:** Continuous wave (CW)
- **Frequency:** 0.15 (MEEP units)
- **Component:** Ez (electric field in z-direction)
- **Position:** x = -8 (left side, inside waveguide)
- **Amplitude:** 10 (amplified for visibility)

### Simulation Parameters
- **Resolution:** 20 pixels/unit
- **Time:** Run until t = 100

---

## Results

### Observations

**Electric Field Distribution:**
- Strong confinement in silicon waveguide (y ≈ 50-70 pixels)
- Oscillating pattern: Red (E > 0) and Blue (E < 0)
- ~10-12 oscillations visible across simulation window
- Minimal field outside waveguide (evanescent decay)

**Key Learnings:**

1. **Light confinement works:**
   - High index contrast (Si/Air: 3.46/1.0) enables strong confinement
   - Light stays within waveguide boundaries

2. **Wavelength in material:**
   - λ_Si = λ_vacuum / n ≈ λ_vacuum / 3.46
   - More oscillations in Si than would be in air
   - Confirms: n determines λ_material

3. **Electromagnetic nature of light:**
   - Red/blue patterns = E field oscillations
   - Not a "particle beam" but a wave
   - E field amplitude varies spatially

---

## What I Learned

### Conceptual Understanding

**Before simulation:**
- Light = abstract concept
- Waveguides = theoretical

**After simulation:**
- Light = oscillating electromagnetic field (E + B)
- Waveguides = physical structures that confine these fields
- Can visualize and predict behavior

### Technical Skills

- MEEP installation and configuration
- Python scripting for photonics
- Electromagnetic field visualization
- Understanding of ε (permittivity) and n (refractive index)

### Challenges Encountered

1. **Initial setup issues:**
   - Conda environment configuration
   - Importing MEEP correctly
   - Solved: `conda install -c conda-forge pymeep`

2. **Visualization problems:**
   - First attempts showed empty plots (simulation too short)
   - Solution: Increased runtime, used CW source

3. **Understanding output:**
   - Confusion about what red/blue meant
   - Learned: Color = E field sign and magnitude

---

## Next Steps

- [x] Compare different materials (glass, polymer) → See simulation 002
- [ ] Simulate curved waveguide (bending losses)
- [ ] Add second waveguide (coupling)
- [ ] Resonator structures (ring, cavity)

---

## Code

See `notebook.ipynb` for complete simulation code.

**Key code snippet:**
```python
import meep as mp

# Geometry
geometry = [
    mp.Block(
        size=mp.Vector3(mp.inf, 1, mp.inf),
        center=mp.Vector3(0, 0, 0),
        material=mp.Medium(epsilon=12)  # Silicon
    )
]

# Source
sources = [
    mp.Source(
        mp.ContinuousSource(frequency=0.15),
        component=mp.Ez,
        center=mp.Vector3(-8, 0, 0),
        amplitude=10
    )
]

# Run simulation
sim = mp.Simulation(
    cell_size=mp.Vector3(20, 6, 0),
    boundary_layers=[mp.PML(thickness=1.0)],
    geometry=geometry,
    sources=sources,
    resolution=20
)

sim.init_sim()
sim.run(until=100)
```

---

## Images

*(Upload your MEEP output images here)*

---

## Notes

**Personal reflection:**

This was my first time "seeing" light as an electromagnetic wave. Before, I only 
understood light conceptually. Now I can visualize how it propagates, how it's 
confined, and why materials matter.

This simulation proved that I can use professional physics tools (MEEP) even as 
a high school student. It's not magic - it's physics + code + patience.

**Foundation for NIANI:** Understanding how light propagates in waveguides is the 
FIRST brick. Neural networks will use these waveguides as connections between 
photonic neurons.

---

*Simulation 001 - The journey begins.*
