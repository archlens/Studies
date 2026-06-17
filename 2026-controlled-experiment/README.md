# 2026 Controlled Experiment — Replication Materials

Replication materials for the paper **"Seeing Is Not Complying: Intentional
Architectural Erosion under Time Pressure despite Continuous Dependency
Visualization"** (Bækgaard, Damgaard, Lungu; IEEE VISSOFT 2026).

We ran a controlled experiment with twenty-five developers on whether ArchLens,
a continuous in-editor dependency visualization, changes how many
architectural dependency-policy violations developers introduce while coding.
Treatment participants used ArchLens; the control group used the same static
documentation without it. Each session closed with a semi-structured group
discussion.

## Contents

- [`ArchLens-VISSOFT2026-ReplicationPackage.pdf`](ArchLens-VISSOFT2026-ReplicationPackage.pdf)
  — the full replication package: participant demographics, the complete
  Spearman correlation matrix, the onboarding script, the group-discussion
  guide, the pre- and post-experiment questionnaires, the task descriptions,
  the `CoDepend` README and delivery guide, the thematic-analysis coding frame
  and theme summary, and the seven group-discussion transcripts.
- [`transcripts/`](transcripts/) — the seven anonymized, English-translated
  group-discussion transcripts as plain text. Speakers are pseudonymous aliases
  (`c01`–`c13` control, `t06`–`t17` treatment, `r01` the interviewer); the
  discussions were conducted in Danish and translated to English.
- [`task-descriptions.md`](task-descriptions.md) — the five tasks (eleven
  subtasks) participants implemented.

The ArchLens tool is open source at <https://github.com/archlens/ArchLens>; the
analysis scripts are at <https://github.com/BabLoRP/data-processing>.

A citable, versioned archive of this package will be deposited on **Zenodo** for
the camera-ready version of the paper.
