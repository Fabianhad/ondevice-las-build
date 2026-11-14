# On Device: LAS — patched build

GitHub Actions workflow that builds [Mesutcydev/ios-local-llm](https://github.com/Mesutcydev/ios-local-llm)'s
"On Device: LAS" app (OnDeviceLAS target, tag `sideload-3.2.6-146` by default) with the local API's
limits for imported GGUF models raised:

| Setting | Upstream 3.2.6 | Default here |
|---|---|---|
| Max output tokens | 256 | 4096 (the app's device safety cap still applies: ~3840–4096, 1536 when hot) |
| llama.cpp context | 4096 | 16384 |

Only `importedGGUFContextTokens` / `importedGGUFMaxOutputTokens` in
`IOSLocalLLM/Services/CodingAssistantService.swift` change; the camera "Lens" profile is untouched.

## Use

1. **Actions** tab → **Build unsigned IPA (raised token limits)** → **Run workflow** (adjust the numbers if needed).
2. Download the `.ipa` artifact from the finished run.
3. Sign and install it with Sideloadly or AltStore using your Apple ID (free accounts: re-sign every 7 days).

If the model fails to load after the change, run again with a smaller context (e.g. output 2048 / context 8192).

The output is unsigned and unofficial. Upstream code is © its authors under its own license.
