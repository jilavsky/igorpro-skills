---
description: "The ThreadGroupCreate function creates a thread group containing nt threads and returns a thread ID number."
slug: /commands/threadgroupcreate
---

<div className="command-signature">

## <strong>ThreadGroupCreate</strong> (<em>nt</em>) {#threadgroupcreate}

</div>

The ThreadGroupCreate function creates a thread group containing *nt* threads and returns a thread ID number. Use the number of computer processors for *nt* when trying to improve computation speed using parallel threads. A background worker might use just one thread regardless of the number of processors.

### *See Also* {#see-also}
[ThreadSafe Functions](/igorpro/programming/programming.md#threadsafe-functions), [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking)