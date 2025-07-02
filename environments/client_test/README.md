# Client Test Environment

This is the default test environment for the Creatures Generator.

## Files

- `prompt.txt`: Base prompt template with placeholders for dynamic attributes
- `attributes.json`: Available colors, passions, and styles for this environment
- `lora/`: Directory for LoRA model files (Phase 2)
- `style_dataset/`: Directory for style reference images (Phase 2)

## Usage

This environment is used by default when `env_id=client_test` is specified in API calls.