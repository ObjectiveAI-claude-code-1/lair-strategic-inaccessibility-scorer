# lair-strategic-inaccessibility-scorer

A scalar function that evaluates how difficult it would be for heroes, government agents, and do-gooders to locate and assault a potential evil lair location. Returns a score from 0 (trivially accessible) to 1 (virtually impregnable).

## Purpose

Every great villain knows that their lair is more than a headquarters—it is a statement, a sanctuary, and a strategic asset. This function provides rigorous, multi-dimensional analysis to help aspiring supervillains, megalomaniacs, and criminal masterminds make data-driven decisions about where to establish the seat of their nefarious operations.

## Input

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `location` | string | Yes | A text description of the potential lair location, including geographic features, terrain, structures, and environmental conditions |
| `villain_profile` | string | No | Optional context about the villain's operational style, resource level, known enemies, and preferences |

## Output

A scalar value between 0 and 1:

- **0.0 - 0.2**: Trivially accessible. Law enforcement could arrive within minutes.
- **0.2 - 0.4**: Marginally defensible. A determined assault would succeed quickly.
- **0.4 - 0.6**: Moderately inaccessible. Significant resources required to breach.
- **0.6 - 0.8**: Highly inaccessible. Would require substantial military intervention.
- **0.8 - 1.0**: Virtually impregnable. Even full military forces would struggle.

## Evaluation Dimensions

The function evaluates locations across four equally-weighted dimensions (25% each):

### 1. Geographic Remoteness
- Distance from major population centers and law enforcement
- Natural barriers: oceans, mountains, deserts, jungle, ice
- Absence of convenient transportation infrastructure
- Inhospitable environmental conditions deterring casual visitors

### 2. Concealment Potential
- Natural camouflage opportunities (volcanic caves, underwater, underground)
- Plausible cover stories for visible surface structures
- Difficulty of satellite surveillance and aerial reconnaissance
- Absence of distinctive thermal, electromagnetic, or acoustic signatures

### 3. Defensive Perimeter
- Natural chokepoints and kill zones for approaching forces
- Terrain favoring defenders over attackers
- Multiple escape routes for emergency evacuation
- Capacity for layered defensive installations

### 4. Counter-Intelligence Value
- Proximity to legitimate traffic providing cover for suspicious activity
- Access to communication infrastructure for monitoring enemies
- Ability to blend logistics with legitimate commerce
- Locations where unusual activity goes unreported

## Example Usage

```json
{
  "location": "A decommissioned Cold War bunker complex in the mountains of Montenegro. Located at 1,800 meters elevation, accessible only by a winding mountain road that becomes impassable in winter. The bunker extends deep into the mountain with multiple underground levels.",
  "villain_profile": "A former intelligence officer with significant financial resources."
}
```

## Example Locations

The function can evaluate diverse location types:

- **Urban**: Warehouses, skyscrapers, underground tunnel networks
- **Remote**: Volcanic islands, Antarctic bases, Arctic fortresses
- **Underwater**: Seafloor habitats, converted oil platforms
- **Orbital**: Space stations, satellite facilities
- **Historical**: Medieval tunnels, ancient monasteries, Cold War bunkers
- **Mobile**: Converted yachts, mobile headquarters

## How It Works

The function uses 16 independent binary evaluations (HIGH/LOW) organized into the four pillars above. Each evaluation uses a vector completion task with an ensemble of LLMs voting on whether the location scores HIGH or LOW for that specific criterion.

The final score is the average of all 16 evaluations, naturally weighting each pillar equally since they each contain 4 evaluations.

*"The supreme art of villainy is to ensure the enemy never finds you at all."*
