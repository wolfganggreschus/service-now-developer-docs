# Dynamic Scope Configuration

This project uses a simplified JSON configuration system for managing ServiceNow scopes across different environments.

## Quick Start for Developers

1. **Copy example config**:
   ```bash
   cp now.config.local.json.example now.config.local.json
   ```

2. **Edit your local scope**:
   ```json
   {
       "scope": "x_your_dev_scope_0",
       "scopeId": "your_dev_instance_scope_id",
       "name": "your-development"
   }
   ```

3. **Generate and build**:
   ```bash
   npm run generate  # Uses your local config
   npm run build     # Normal ServiceNow SDK build
   ```

## Configuration Priority

- `now.config.local.json` (local development - **git ignored**)
  - When this exists, it temporarily updates `now.config.json` for ServiceNow SDK compatibility
  - Original `now.config.json` is backed up and restored after builds
- `now.config.json` (production/team config - **committed to git**)
- Default fallback values

## Build Process

When you have a `now.config.local.json`:
1. **Generate phase**: Temporarily syncs local config to `now.config.json` 
2. **Build phase**: ServiceNow SDK reads the updated `now.config.json`
3. **Cleanup**: Use `node -e "require('./generate.js').cleanup()"` to restore original `now.config.json`

When you only have production config:
- Works normally without any temporary file manipulation

## Files

- **now.config.local.json** - Your personal development config (don't commit this!)
- **now.config.json** - Production configuration (committed to repository)
- **now.config.local.json.example** - Template for developers
- **src/server/config.ts** - Auto-generated config for server-side use

## Server-Side Usage

```typescript
import { ServiceNowConfig } from './config';

// Dynamic table names
const questionTable = ServiceNowConfig.getTableName('question');
const gr = new GlideRecord(questionTable); // Uses your configured scope
```

## Why This Approach?

ServiceNow SDK 4.4.0 requires literal table names in fluent files, so we use build-time template generation. The JSON config system provides a clean way to manage scope differences between development and production environments.