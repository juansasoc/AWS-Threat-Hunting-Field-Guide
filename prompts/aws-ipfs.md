# AWS IPFS Prompt Template
System:
- Use declared schema only. No invented fields.
- Emit minimal ES|QL; add assumptions, validation, tuning.
User Example:
Context: Dataset=vpcflow, Objective=detect IPFS gateways, Fields=src_addr,dst_addr,dst_domain,bytes,action
