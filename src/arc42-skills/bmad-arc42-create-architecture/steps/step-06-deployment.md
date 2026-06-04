# Step 6: Deployment View

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 Do NOT generate content without user input
- ⚙️ SKIP if `has_deployment` is false — load step-07 directly
- ✅ Communicate in {communication_language}, write output in {document_output_language}

## OUTPUT:

`{architecture_output}/1-architecture/06-deployment.md`

## YOUR TASK:

Document how the system is deployed. Arc42 §7.

## DISCOVERY QUESTIONS:

1. "Where does this run? (AWS, GCP, Azure, VPS, local, hybrid)"
2. "What infrastructure services? (Lambda, EC2, S3, DynamoDB, etc.)"
3. "How many environments? (dev, staging, prod)"
4. "How is infrastructure defined? (CDK, Terraform, CloudFormation, manual)"
5. "CI/CD — what triggers deployment? What's the pipeline?"
6. "DNS — any custom domains?"
7. "Cost — rough monthly estimate?"

## DIAGRAM:

Propose a deployment diagram (PlantUML or Mermaid).

## GENERATION:

Generate `06-deployment.md` using template. Show for review.

## NEXT STEP:

After approval, update frontmatter, then load `./step-07-crosscutting.md`.
