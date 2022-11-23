def dotnet_build(ref,context = ".", version = "latest"):
    docker_build(
        ref = ref,
        context = context,
        dockerfile_contents = "                                 \n\
            from mcr.microsoft.com/dotnet/sdk:" + version + "   \n\
            workdir app                                         \n\
            copy . .                                            \n\
            run dotnet restore                                  \n\
            env DOTNET_WATCH_RESTART_ON_RUDE_EDIT=true          \n\
            entrypoint dotnet watch run --no-restore            \n\
        ",
        live_update = [
            fall_back_on([
             context + "/program.csproj",
             context + "/appsettings.json",
            ]),
            sync(context, "/app"),
        ],
    );

def vue_build(ref,context = ".", version = "latest"):
    docker_build(
        ref = ref,
        context = context,
        dockerfile_contents = "                                         \n\
            from reg.govcloud.dk/gcproxy/library/node:" + version + "   \n\
            workdir app                                                 \n\
            copy . .                                                    \n\
            run npm install vite                                        \n\
            entrypoint node_modules/.bin/vite                           \n\
        ",
        live_update = [
            fall_back_on([
            context + "/package.json",
            context + "/package-lock.json",
            ]),
            sync(context, "/app"),
        ],
    );

