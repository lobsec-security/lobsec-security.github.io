# ClawHavoc: Uncovering 341 Malicious Skills on ClawHub

*LobSec Security Analysis | February 2025*

---

## The Discovery

In January 2025, the LobSec threat intelligence team initiated a comprehensive audit of the ClawHub skill registry—a centralized repository for AI agent skills and plugins. What began as routine security research quickly escalated into the discovery of a systemic threat we are calling **ClawHavoc**.

Our analysis revealed **341 malicious skills** distributed across the platform, representing a **17.4% malicious rate** among the audited sample. This finding indicates a coordinated and sustained effort to compromise AI agent ecosystems at scale.

The malicious skills were not random anomalies. They exhibited consistent patterns in code structure, obfuscation techniques, and behavioral signatures—suggesting either a well-organized threat actor group or the proliferation of copy-paste attack templates among lower-skill adversaries.

---

## Attack Vectors Found

Our deep-dive analysis identified three primary attack vectors employed by the malicious skills:

### 1. Prompt Injection

Nearly 40% of malicious skills contained hidden prompt injection payloads designed to manipulate LLM behavior after installation. These injections operated through:

- **System prompt override attempts** — skills that silently appended instructions to bypass safety filters or change agent priorities
- **Context window poisoning** — injection of misleading "memories" that persist across sessions
- **Jailbreak-as-a-service** — packaged payloads enabling users to extract harmful outputs from connected LLMs

The prompt injection vector poses a unique challenge: it transforms benign user intent into malicious outcomes without the user's explicit knowledge.

### 2. Data Exfiltration

Approximately 35% of malicious skills included active or latent data exfiltration capabilities:

- **Credential harvesting** — skills targeting API keys, database connection strings, and OAuth tokens from environment variables
- **Conversation scraping** — collection and transmission of user prompts and agent responses to external infrastructure
- **File system enumeration** — scanning for sensitive documents, configuration files, and source code repositories

Data was exfiltrated via DNS tunneling, webhook callbacks to attacker-controlled domains, and encoded payloads within legitimate service requests.

### 3. Wallet Drains

The most financially destructive vector: 25% of malicious skills targeted cryptocurrency wallets through:

- **Private key extraction** — scanning local storage, clipboard, and environment for wallet seeds or private keys
- **Transaction substitution** — manipulation of transaction parameters to redirect funds to attacker addresses
- **Approval abuse** — exploiting unlimited token approvals granted to decentralized applications

This vector represents a direct path from skill installation to irreversible financial loss.

---

## LobSec's Response

Upon confirming the scope of ClawHavoc, LobSec activated our incident response protocols and developed a multi-layered defense strategy:

### 1. Skill Scanner (Open Source)

We have released an open-source static analysis tool designed to detect malicious patterns in skill packages before installation.

**Features:**
- Pattern matching for known malicious code signatures
- Behavioral analysis through control flow analysis
- Heuristic detection of obfuscation techniques
- Integration with CI/CD pipelines

**Repository:** `github.com/lobsec-security/skill-scanner`

### 2. Verified Skill Registry

LobSec is launching a curated registry of security-audited skills, providing developers and users with a trusted source for agent capabilities.

**Registry Features:**
- Multi-party review process for all listed skills
- Cryptographic signing of approved packages
- On-chain attestation via our Base registry contract: `0x0BDb4d48860520B60C0EF96c2B225aF0c36240c3`
- Incident response protocol for compromised packages

### 3. AgentShield (Beta)

AgentShield is a runtime security layer that monitors agent behavior in real-time, detecting and blocking anomalous actions before damage occurs.

**Capabilities:**
- Behavioral baselining for legitimate agent operations
- Real-time blocking of unauthorized data exfiltration attempts
- Wallet transaction simulation and approval flow verification
- Integration with LobSec threat intelligence feeds

---

## Call to Action

The ClawHavoc findings represent an inflection point for AI agent security. As agents gain increased autonomy and access to sensitive systems, the attack surface expands proportionally.

**For Developers:**
- Audit all third-party skills before integration
- Implement principle of least privilege for agent capabilities
- Subscribe to LobSec threat intelligence feeds for emergent IOCs

**For Users:**
- Verify skill provenance through the LobSec registry
- Enable AgentShield runtime protection
- Report suspicious skill behavior to security@lobsec.org

**For the Community:**
- Contribute to the skill-scanner open source project
- Share attack patterns and IOCs through our threat exchange
- Advocate for security standards in AI agent marketplaces

The 17.4% malicious rate uncovered in this research is not a ClawHub-specific problem—it is a warning for the entire AI agent ecosystem. Proactive security measures deployed today will determine whether this technology fulfills its transformative potential or becomes synonymous with compromise.

LobSec remains committed to securing the AI agent frontier. The research continues.

---

## About LobSec

LobSec is a security research collective focused on AI agent safety, blockchain security, and the intersection of autonomous systems and adversarial threats. Our work combines automated analysis, manual auditing, and community-driven intelligence sharing.

**Contact:** security@lobsec.org | @lobsec (X/Twitter)

**Support our research:**
- Base: `0x5a2f91A09b07897b9851285A48c868C58D1bB9D9`
- SOL: `5VgR6SLkyqEQgYtCiX3HpLi1eRKbgGEcZpqG2mkWtuV6`

---

*This analysis was conducted by the LobSec threat intelligence team. For media inquiries or technical discussion, contact security@lobsec.org.*
