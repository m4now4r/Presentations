At Security Bootcamp 2025 – Resilience, held in Hue City, Vietnam, from 12–14 September 2025, I presented *“APT35: The Silent Adversary Under the Radar”*, a technical deep dive into the infection chain, malware architecture, and notable techniques employed by the Iranian-linked APT35 threat group.

Rather than focusing solely on the malware’s execution flow, the presentation explored several technical aspects that make these samples challenging to analyze, including custom string encryption, anti-analysis techniques, and the abuse of Windows COM to bridge native code with .NET components.

**1. A Brief Look at APT35**

The presentation began with an overview of APT35, a threat actor known under multiple aliases, including Charming Kitten, Phosphorus, Mint Sandstorm, Magic Hound, NewsBeef, and Educated Manticore.

APT35 is widely assessed as an Iranian state-sponsored threat group, with reported links to the Islamic Revolutionary Guard Corps (IRGC). The group has conducted numerous campaigns over the years, targeting organizations and individuals across different sectors and regions.

This section provided a concise overview of APT35’s evolution, notable campaigns, and publicly documented activities, establishing the broader context for the technical analysis that followed.

**2. Infection Chain and Attack Techniques**

The analyzed APT35 sample presented at SBC 2025 demonstrated a multi-stage infection chain designed to conceal malicious activity from the victim.

The attack begins with a malicious .LNK shortcut masquerading as a Microsoft Edge icon. Once executed, the shortcut launches a legitimate-looking PDF decoy document to distract the victim while the malicious execution continues in the background.

Behind the decoy, malicious DLL components are loaded and subjected to multiple layers of decryption and execution. Eventually, the infection chain reaches PowerLess, a script-based component used to perform subsequent malicious activities, including data theft from the compromised system.

The presentation reconstructed this chain step by step, highlighting how each stage contributes to stealth, execution, and evasion.

**3. Deep Dive into Notable Techniques**
**3.1 Custom String Decryption Based on TEA32**

To hinder static analysis and automated string extraction, APT35 samples employ an additional protection layer consisting of custom string-decryption routines based on TEA32 (Tiny Encryption Algorithm). Each decryption routine uses its own cryptographic key and is designed to process strings of specific lengths. Furthermore, multiple variants of these routines implement different control logic, making it significantly more difficult to build a generic automated string-extraction mechanism.
An interesting consequence of this approach is that the AppCall technique, which I previously discussed at Security Bootcamp 2024, becomes considerably less effective against samples employing this particular protection mechanism.
To overcome this limitation, I developed an IDAPython-based automation framework to streamline the string-recovery process. The script is designed to:

    - Automatically identify potential string-decryption functions.
    - Locate all relevant cross-references (xrefs) to these routines.
    - Dynamically establish conditional breakpoints at appropriate execution points.
    - Control the debugging process programmatically.
    - Recover decrypted strings directly from runtime memory.
    - Provide an extensible approach that can be adapted to different variants of the malware.

This approach shifts the analysis from manually reversing each decryption routine toward a more scalable and automation-oriented workflow for malware research.

**3.2 Abusing COM to Invoke Functions from a .NET DLL**

Another notable technique covered in the presentation was the abuse of Microsoft Component Object Model (COM) to invoke functionality implemented inside a .NET DLL.
COM is a core Windows technology introduced in the early 1990s to enable standardized communication between software components. It was originally designed to facilitate interoperability between applications—for example, embedding an Excel chart inside a Microsoft Word document.
However, the same flexibility and abstraction provided by COM can also be abused by malware. From a malware-analysis perspective, COM-based execution presents an additional challenge because traditional API monitoring and some sandbox environments may have limited visibility into COM interface interactions. This can make the execution chain less transparent and potentially contribute to anti-analysis or anti-sandbox behavior.
In this section, I walked through the COM architecture relevant to the sample and demonstrated the reverse-engineering process used to reconstruct the COM-related structures and interfaces.

A key challenge is that many of the interfaces involved are not readily available in IDA Pro’s type information database. Consequently, accurately reconstructing the relevant COM interfaces, virtual function tables, and associated structures becomes an essential step in understanding the malware’s execution flow.
By rebuilding these structures during reverse engineering, it becomes possible to reveal how a native DLL communicates with and invokes functionality implemented inside a .NET DLL through COM interfaces—a technique that would otherwise remain obscured behind indirect calls and unfamiliar function-pointer structures.Closing Perspective
When it comes to APTs, don’t focus too much on the word “Advanced.” They aren’t always advanced; they are simply “advanced enough” for their targets.

The APT35 case study demonstrates that effective threat actors do not necessarily need to rely on cutting-edge techniques. Instead, they can combine relatively well-known techniques—such as custom encryption, obfuscation, multi-stage execution, and abuse of legitimate Windows technologies like COM—in ways that are sufficiently effective against their intended targets.

From a malware-analysis perspective, the challenge is therefore not only understanding how sophisticated a technique is, but also understanding how effectively the adversary combines these techniques to evade detection, complicate analysis, and achieve its objectives.
