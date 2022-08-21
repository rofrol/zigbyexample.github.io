---
layout: default
title: Spawning Subprocess
nav_order: 3
permalink: /spawn_subprocess
---

[subprocess.zig](src/subprocess.zig)

```zig
const std = @import("std");

test {
    const args = [_][]const u8{ "ls", "-al" };

    var process = std.ChildProcess.init(&args, std.testing.allocator);
    std.debug.print("Running command: {s}\n", .{args});
    try process.spawn();

    const ret_val = try process.wait();
    try std.testing.expectEqual(ret_val, .{ .Exited = 0 });
}

```