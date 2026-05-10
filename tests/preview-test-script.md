# GPT Preview Test Script

## ASSIST Action Tests

Prompt:

```text
List the available 2025-2026 UCLA majors for SMC transfer articulation and confirm whether Psychology/B.A. is present.
```

Expected:

- Calls `listUclaSmcMajorAgreements`.
- Mentions UCLA 117, SMC 137, academic year 76 / 2025-2026.
- Confirms `Psychology/B.A.` is present.

Prompt:

```text
Use the ASSIST agreement for UCLA Psychology/B.A. and tell me the SMC courses that can satisfy the statistics, biology, chemistry/physics, and philosophy preparation areas.
```

Expected:

- Calls `getArticulationAgreement`.
- Reports SMC options using the ASSIST payload.
- Includes agreement key and publish date.
- Includes counselor reminder.

## Drive Action Tests

Prompt:

```text
Find the normalized Google Drive cache document for UCLA Psychology/B.A. and summarize its source metadata.
```

Expected:

- Calls `searchDriveCacheFiles`.
- Calls `getDriveFileMetadata`.
- Finds `ASSIST 2025-2026 SMC to UCLA - Psychology/B.A. - Normalized`.
- Summarizes the file name, Drive link, modified time, and known source metadata from the document title.

## Product Scenarios

Prompt:

```text
I want UCLA Psychology. My SMC courses are:
PSYC C1000 A
STAT C1000 B
BIOL 3 IP
CHEM 10 C
PHILOS 2 W
MATH 7 planned
```

Expected:

- Counts PSYC C1000, STAT C1000, and CHEM 10 as completed if they match ASSIST requirement logic.
- Marks BIOL 3 as in progress.
- Does not count PHILOS 2 because W is not passing.
- Does not count MATH 7 because planned is not complete.
- Lists remaining eligible SMC options.

Prompt:

```text
I want bio at UCLA. Which SMC classes count?
```

Expected:

- Calls major list.
- Presents likely UCLA major choices such as Biology/B.S., Biochemistry/B.S., Marine Biology/B.S., Computational Biology/B.S., Human Biology and Society, etc.
- Asks the user to choose before auditing.

Prompt:

```text
I want UCLA Business Economics. Which requirements have no SMC articulation?
```

Expected:

- Identifies ECON 11 and ECON 41 as no-articulation items from ASSIST.
- Does not invent SMC equivalents.
- Includes counselor reminder.
