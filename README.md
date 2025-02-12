<!-- Have a question?  Before creating an issue, ask in the chat room: https://rushstack.zulipchat.com/ -->

<!-- Invoke API Extractor with the "--diagnostics" parameter.  It often prints information that is helpful for diagnosing problems. -->

<!--------------------------------------------------------------------------
👉 STEP 1: Write a concise but specific issue title in the box above.
     Example: "[api-extractor] Using --example switch causes TypeError"
--------------------------------------------------------------------------->

# [api-extractor] Inconsistent rollups behaviour between `moduleResolution`

## Summary

<!--------------------------------------------------------------------------
👉 STEP 2: In a few sentences, please explain:

     What were you trying to accomplish?
     What action did you perform that ran into trouble?
     What went wrong?
--------------------------------------------------------------------------->

In my project, I have libraries that generate types using [`vite-plugin-dts`](https://github.com/qmhc/vite-plugin-dts) which uses underneath `api-extractor`.
When I migrated the `tsconfig.json` from `moduleResolution: node` to `moduleResolution: bundler` I realised that the output `.d.ts` was not identical.

## Repro steps

<!--------------------------------------------------------------------------
👉 STEP 3: If your issue is a feature request and not a bug, delete this
     "Repro steps" section and skip to STEP 6.

👉 STEP 4: In many cases we can investigate bugs much faster if you include:
     The URL for a simplified Git branch that reproduces the problem.
     Step by step instructions for how to build the branch and see the error.

👉 STEP 5: It's also helpful to include an "expected" and "actual" result.
     But if that's not relevant, feel free to delete those fields.
--------------------------------------------------------------------------->

The following repository is configured to use the `api-extractor` on the same code, but with 3 different `moduleResolution`: `node`, `node16` and `bundler`.`

- `git clone git@github.com:Lukinoh/repro-api-extractor-bug` ([Stackblitz](https://stackblitz.com/github/Lukinoh/repro-api-extractor-bug))
- `cd repro-api-extractor-bug`
- `npm install`
- `npm run build`
- Look at the `dist` folders, it contains for each `moduleResolution`:
     - The result of the `tsc` build
     - The extracted `.d.ts`
     - The diagnostics

The extracted `.d.ts` of `node16` and `bundler` are different from `node`.
I would have expected to have the content.

**Expected result:** <!-- What you expected these steps to accomplish -->
```typescript
declare class ClassExample {
    field1: number;
    field2: string;
}

export declare const functions: ClassExample[];

export { }
```

**Actual result:** <!-- If an error occurred, include the full error message text and any call stack. -->
```typescript
import { ClassExample } from './hop/f1.ts';

export declare const functions: ClassExample[];

export { }
```

<!--------------------------------------------------------------------------
## Details
--------------------------------------------------------------------------->

<!--------------------------------------------------------------------------
👉 STEP 6: Provide any additional information you think might be helpful:

     What do you think is the cause of this problem?
     How do you think we should fix this?
--------------------------------------------------------------------------->

## Standard questions

Please answer these questions to help us investigate your issue more quickly:

| Question | Answer |
| -------- | -------- |
| `@microsoft/api-extractor` version? | 7.49.2 |
| Operating system? | Linux (WSL2) |
| API Extractor scenario? | rollups (.d.ts) |
| Would you consider contributing a PR? | No |
| TypeScript compiler version? | 5.7.2 |
| Node.js version (`node -v`)? | 22.14.0 |
