# dotenv zig 0.14.0

- dotenv is a super simple single file zig library for parsing a `.env` file.
- implementation is < 100 lines
- Support for key-value pairs separated by `=` in the `.env` file.
- No dependencies

## Usage

0. with zon: zig fetch --save "thisrepo/hash"
   add in build.zig the name of the module is "dotenv"

1. Create a `.env` file in your project or executable directory:

   ```sh
   # .env
   MY_ENV_VAR=hello
   ANOTHER_VAR=world
   ```

2. Use dotenv to read the environment variable:

   ```zig
   const dotenv = @import("dotenv");
   pub fn main() !void {
      const alloc = std.testing.allocator;
      // read the env file
      var file = try std.fs.cwd().openFile(".env", .{});
      defer file.close();
      const content = try file.readToEndAlloc(alloc, 1024 * 1024);
      defer alloc.free(content);
      // parse the env file
      var env: Env = try Env.init(alloc, content);
      defer env.deinit();
      std.debug.print("{s}\n", .{env.get("password").?});
      // Use the environment variables
      // ...
   }
   ```

## Contributing

Contributions are welcome! Fork the repository and submit a pull request.

## License

dotenv-zig is licensed under the MIT License. See [LICENSE](LICENSE) for details.
