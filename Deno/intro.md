# What is Deno

Deno is a simple, modern and secure runtime for JavaScript and TypeScript that uses V8 and is built in Rust. - https://deno.land/

## Install deno (MacOS, Linux)

More options are [here](https://deno.land/)

```bash
# [Caution] vscode deno plugin error may occur later
$ curl -fsSL https://deno.land/x/install/install.sh | sh

# Via brew (Recommended)
$ brew install deno
```

## Simple example

From terminal

```bash
$ deno run https://deno.land/std/examples/welcome.ts
Welcome to Deno 🦕
```

## File Server example

If you skip these options (`--allow-net --allow-read`), You will encounter an error.

```bash
# Wrong approach
$ deno run https://deno.land/std/http/file_server.ts
error: Uncaught PermissionDenied: read access to "/Users/seokjepark/Code/TIL", run again with the --allow-read flag

# Right approach
$ deno run --allow-net --allow-read https://deno.land/std/http/file_server.ts
HTTP server listening on http://0.0.0.0:4507/
```

## Write File example

TextEncoder is an Wep API which generate a byte stream with UTF-8 encoding.
- WriteFile returns promise
- Await don't have to be in a Async function because Deno handles this.

```typescript
// createFile.ts
const encoder = new TextEncoder();
const greetText = encoder.encode('Hello Deno\nWhere are you?');

await Deno.WriteFile('greet.txt', greeText);
```

Execute above with deno
```bash
$ deno run createFile.ts
error: Uncaught PermissionDenied: write access to "/Users/seokjepark/Code/deno-pg/greet.txt", run again with the --allow-write flag

$ deno run --allow-write createFile.ts
Hello Deno
Where are you?
```

## Install

`deno install {script}` Install script as an executable.

```bash
$ deno install --allow-net --allow-read https://deno.land/std/http/file_server.ts
✅ Successfully installed file_server
/Users/seokjepark/.deno/bin/file_server

# To excecute:˜
$ file_server
HTTP server listening on http://0.0.0.0:4507/
```

## Uninstall

```bash
$ rm `which deno`
```

## VSCode Extensions

[Issue] When the exclamation point is displayed in the lower right deno icon, restart vscode.

https://github.com/denoland/vscode_deno

## Reference site

- [Deno Official site](https://deno.land/)
- [Deno Crash Course](https://morioh.com/p/05cffb094fa3?fbclid=IwAR2PMP66qOT4NfAPSzG-3YS7IRoQ4kulguBZ-nh4YasMAkmZMxHx-cfuYxw)
- []()
- []()
