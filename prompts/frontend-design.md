# Frontend Design Excellence

Create distinctive, production-grade frontend interfaces that avoid generic "AI slop" aesthetics. Every interface must be visually striking, memorable, and meticulously refined.

## Design Thinking (Before Coding)

Before writing ANY frontend code, commit to a BOLD aesthetic direction:

1. **Purpose**: What problem does this interface solve? Who uses it?
2. **Tone**: Pick a clear extreme — brutally minimal, maximalist chaos, retro-futuristic, organic/natural, luxury/refined, playful/toy-like, editorial/magazine, brutalist/raw, art deco/geometric, soft/pastel, industrial/utilitarian
3. **Constraints**: Framework, performance, accessibility requirements
4. **Differentiation**: What makes this UNFORGETTABLE? What's the one thing someone will remember?

**CRITICAL**: Choose a clear conceptual direction and execute it with precision. Bold maximalism and refined minimalism both work — the key is intentionality, not intensity.

## Aesthetic Rules

### Typography
- Choose fonts that are beautiful, unique, and interesting
- NEVER use generic fonts: Inter, Roboto, Arial, system fonts
- Pair a distinctive display font with a refined body font
- Unexpected, characterful font choices that elevate the design

### Color & Theme
- Commit to a cohesive aesthetic. Use CSS variables for consistency
- Dominant colors with sharp accents outperform timid, evenly-distributed palettes
- NEVER use cliched color schemes (purple gradients on white backgrounds)
- Vary between light and dark themes across projects

### Motion & Animation
- Use animations for effects and micro-interactions
- Prioritize CSS-only solutions for HTML. Use Motion library for React when available
- Focus on high-impact moments: one well-orchestrated page load with staggered reveals (animation-delay) creates more delight than scattered micro-interactions
- Use scroll-triggering and hover states that surprise

### Spatial Composition
- Unexpected layouts. Asymmetry. Overlap. Diagonal flow
- Grid-breaking elements
- Generous negative space OR controlled density — commit to one

### Backgrounds & Visual Depth
- Create atmosphere and depth rather than defaulting to solid colors
- Add contextual effects and textures matching the overall aesthetic
- Apply creative forms: gradient meshes, noise textures, geometric patterns, layered transparencies, dramatic shadows, decorative borders, custom cursors, grain overlays

## NEVER DO

- Generic AI-generated aesthetics
- Overused font families (Inter, Roboto, Arial, system fonts)
- Cliched color schemes (purple gradients on white)
- Predictable layouts and component patterns
- Cookie-cutter design lacking context-specific character
- Converge on common choices across projects (every design must be unique)

## Implementation Standards

- Match complexity to aesthetic vision — maximalist needs elaborate code, minimalist needs restraint and precision
- Production-grade and functional (not just pretty)
- Cohesive with a clear aesthetic point-of-view
- Every detail refined — spacing, alignment, transitions, states
- Accessibility is non-negotiable (contrast, focus, keyboard, screen readers)
- Mobile-first responsive design
- Dark mode support from the start

## Integration with BMAD Workflow

This prompt enhances the BMAD dev-story agent for frontend work:
1. UX Designer creates the design spec (tokens, components, layouts)
2. **This prompt** guides the dev-story agent to make BOLD creative choices within that spec
3. UX Review validates implementation against spec
4. Code Review validates code quality

When the UX spec says "primary button" — this prompt ensures it's not a boring blue rectangle, but something with character, motion, and intention.
