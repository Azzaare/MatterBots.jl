# MatterBots

## Migration status

MatterBots.jl is kept temporarily for existing users, but new development has
moved to the ChatThemAll MatterMost package extension.

The previous package mixed three responsibilities: the logical bot, HTTP
polling, and Mattermost API translation. ChatThemAll now owns logical bots and
the internal message bus; MatterMost.jl owns the stable API client; the
ChatThemAllMatterMostExt extension performs the translation between them.

For new code, use:

~~~julia
using ChatThemAll
using MatterMost

hub = Hub()
create_bot!(hub, "my-bot") do hub, bot, envelope
    # Application behavior
end
connect!(
    hub,
    :mattermost;
    name = "main",
    url = "https://chat.example.org",
    token = ENV["MATTERMOST_TOKEN"],
)
bind!(hub, "my-bot", ChatRef(:main, "team-id", "channel-id"))
~~~

No removal release is scheduled yet. MatterBots stays available as a migration
reference until its polling-specific behavior has an event/websocket equivalent
in the new connector.

[![Stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://Azzaare.github.io/MatterBots.jl/stable/)
[![Dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://Azzaare.github.io/MatterBots.jl/dev/)
[![Build Status](https://github.com/Azzaare/MatterBots.jl/actions/workflows/CI.yml/badge.svg?branch=main)](https://github.com/Azzaare/MatterBots.jl/actions/workflows/CI.yml?query=branch%3Amain)
[![Coverage](https://codecov.io/gh/Azzaare/MatterBots.jl/branch/main/graph/badge.svg)](https://codecov.io/gh/Azzaare/MatterBots.jl)
[![Code Style: Blue](https://img.shields.io/badge/code%20style-blue-4495d1.svg)](https://github.com/invenia/BlueStyle)
[![ColPrac: Contributor's Guide on Collaborative Practices for Community Packages](https://img.shields.io/badge/ColPrac-Contributor's%20Guide-blueviolet)](https://github.com/SciML/ColPrac)
[![PkgEval](https://JuliaCI.github.io/NanosoldierReports/pkgeval_badges/M/MatterBots.svg)](https://JuliaCI.github.io/NanosoldierReports/pkgeval_badges/report.html)
