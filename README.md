### 1.1 - SvelteKit Project Setup

https://courses.huntabyte.com/view/courses/modern-saas/1887088-module-1-project-setup/6175530-1-1-sveltekit-project-setup

https://github.com/huntabyte/modern-saas/blob/starter-code/.prettierrc#L6 has `prettier-plugin-tailwindcss` but https://github.com/huntabyte/modern-saas/blob/starter-code/package.json does not have `prettier-plugin-tailwindcss`.

After `git clone --single-branch --branch starter-code https://github.com/huntabyte/modern-saas.git` going to `src/lib/index.ts` and writing some JS, on save, prettier does not format it.

```bash
["INFO" - 5:15:35 PM] Formatting file:///.../modern-saas/src/lib/index.ts
["INFO" - 5:15:35 PM] Using config file at '/.../modern-saas/.prettierrc'
```

Now, when I do `pnpm install prettier-plugin-tailwindcss` it complains about a version mismtach to `prettier`.

When I remove `prettier-plugin-tailwindcss` from `.prettierrc` like so, it works.

```json
{
	"useTabs": true,
	"singleQuote": false,
	"trailingComma": "none",
	"printWidth": 100,
	"plugins": ["prettier-plugin-svelte"],
	"pluginSearchDirs": false,
	"overrides": [
		{
			"files": "*.svelte",
			"options": {
				"parser": "svelte",
				"svelteIndentScriptAndStyle": true,
				"svelteStrictMode": false,
				"svelteSortOrder": "scripts-markup-styles-options"
			}
		}
	],
	"bracketSameLine": true
}
```

@huntabyte please tell me how to exactly install `pnpm install prettier-plugin-tailwindcss` with the exact version needed to that prettier and `prettier-plugin-svelte` as well **`prettier-plugin-tailwindcss`** work nicely together, thank you.

### 1.2 - Supabase Local Development

`pnpx supabase init`

`zsh: command not found: pnpx`

<a href="https://stackoverflow.com/a/70266473">https://stackoverflow.com/a/70266473</a>

<a href="https://pnpm.io/cli/dlx">https://pnpm.io/cli/dlx</a>

in .zshrc

`alias px="pnpm dlx"`

`px supabase init --debug`

```bash
Packages: +22
++++++++++++++++++++++
Progress: resolved 22, reused 22, downloaded 0, added 22, done
Supabase CLI 1.93.0
Generate VS Code workspace settings? [y/N] y
Finished supabase init.
```

`px supabase start`

```bash
Packages: +22
++++++++++++++++++++++
Progress: resolved 22, reused 22, downloaded 0, added 22, done
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/_ping": dial unix /var/run/docker.sock: connect: permission denied
  in github.com/supabase/cli/internal/utils.AssertDockerIsRunning:50
  in github.com/supabase/cli/internal/start.Run:37
Try rerunning the command with --debug to troubleshoot the error.
```

<a href="https://www.digitalocean.com/community/questions/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket">https://www.digitalocean.com/community/questions/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket</a>

`sudo groupadd docker`

```bash
sudo groupadd docker
[sudo] password for user:
groupadd: group 'docker' already exists
```

`sudo usermod -aG docker ${USER}`

log out

log in

`docker run hello-world`

```bash
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
719385e32844: Pull complete
Digest: sha256:dcba6daec718f547568c562956fa47e1b03673dd010fe6ee58ca806767031d1c
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

`px supabase start`

works from external terminal, not in vscode

```bash
px supabase start
Packages: +22
++++++++++++++++++++++
Progress: resolved 22, reused 22, downloaded 0, added 22, done
Error response from daemon: toomanyrequests: Rate exceeded
Retrying after 4s: public.ecr.aws/supabase/postgres:15.1.0.103
15.1.0.103: Pulling from supabase/postgres
01085d60b3a6: Pull complete
097a70b5f298: Pull complete
08a5295336b6: Pull complete
8c5e5831dc61: Pull complete
b2e1ecd3d752: Pull complete
af158ba5cb38: Pull complete
87c407b8b319: Pull complete
3ac6f9ab7578: Pull complete
2a6051e5ddc0: Pull complete
2f769da8470e: Pull complete
16adeaf061a3: Pull complete
f4522def5346: Pull complete
fc4831d5008d: Pull complete
7c7bccee5eb4: Pull complete
d1f08b4bfc3c: Pull complete
fac0e7ab1a7e: Pull complete
00f6c46ca39e: Pull complete
2c2e3a137b74: Pull complete
255d332e1d28: Pull complete
13169b0473ab: Pull complete
73624787c2f6: Pull complete
91fe6789b0c1: Pull complete
977b01217d91: Pull complete
Digest: sha256:fe920f18b63d5719a9e0edeebe503131f3025f3e554c1c7487384525b5fc3ebc
Status: Downloaded newer image for public.ecr.aws/supabase/postgres:15.1.0.103
v0.40.4: Pulling from supabase/storage-api
31e352740f53: Pull complete
c017600940c6: Pull complete
c9f8586f07bd: Pull complete
ee16df044bfc: Pull complete
1fbf70d2de34: Pull complete
e8ba86f63bbf: Pull complete
9bda86230051: Pull complete
560fa8c48f98: Pull complete
e4743a95028c: Pull complete
Digest: sha256:6646a6cce0eddaad996ed97fdb3f6903aaae6af87dbf19474677e78b1a08e287
Status: Downloaded newer image for public.ecr.aws/supabase/storage-api:v0.40.4
v2.82.4: Pulling from supabase/gotrue
4db1b89c0bd1: Pull complete
a7d5384f9a85: Pull complete
8844c0117649: Pull complete
1d4f7cd41324: Pull complete
55257c889105: Pull complete
Digest: sha256:2e4cf4e090ad0128a7e7a9fa468846c9116e000cc7bebe7a12d8acc6ad75c1be
Status: Downloaded newer image for public.ecr.aws/supabase/gotrue:v2.82.4
Seeding data supabase/seed.sql...
2.8.1: Pulling from supabase/kong
213ec9aee27d: Pull complete
a70653f7a2d5: Pull complete
531e3bd93090: Pull complete
814dd06d26c7: Pull complete
Digest: sha256:1b53405d8680a09d6f44494b7990bf7da2ea43f84a258c59717d4539abf09f6d
Status: Downloaded newer image for public.ecr.aws/supabase/kong:2.8.1
3.0.3: Pulling from supabase/inbucket
530afca65e2e: Pull complete
866f56904284: Pull complete
e356c9130232: Pull complete
8d4341af276d: Pull complete
82a73217a072: Pull complete
64b833ffe729: Pull complete
a77af8706e66: Pull complete
9c842edb6049: Pull complete
Digest: sha256:dc912ab76de647ca2a363fe285515e512e964cf699166773f3c2c73f5e7f71c0
Status: Downloaded newer image for public.ecr.aws/supabase/inbucket:3.0.3
v2.10.1: Pulling from supabase/realtime
3f9582a2cbe7: Pull complete
99f383335fd5: Pull complete
5c7630b3eea2: Pull complete
387961c45922: Pull complete
1c628aa8f3d3: Pull complete
773700217cb3: Pull complete
eeb47806e6fa: Pull complete
e6f7afe35e1b: Pull complete
2d21e977d193: Pull complete
24218f77a865: Pull complete
d7233802cc80: Pull complete
931fb51461dd: Pull complete
Digest: sha256:e217412dabddae0ea838127350e52b71e82e96b24ab171713afcae8dd0bc21ec
Status: Downloaded newer image for public.ecr.aws/supabase/realtime:v2.10.1
v11.1.0: Pulling from supabase/postgrest
e20ce8189632: Pull complete
Digest: sha256:86fc4a9b56702daefeb238130bfee603fc7b47438333286ec7a23448801707fd
Status: Downloaded newer image for public.ecr.aws/supabase/postgrest:v11.1.0
v3.8.0: Pulling from supabase/imgproxy
bd159e379b3b: Pull complete
6309c66995c3: Pull complete
afc82c51c69d: Pull complete
053e09c75ec1: Pull complete
fc6c361fe360: Pull complete
901d40e1841c: Pull complete
Digest: sha256:0facd355d50f3be665ebe674486f2b2e9cdaebd3f74404acd9b7fece2f661435
Status: Downloaded newer image for public.ecr.aws/supabase/imgproxy:v3.8.0
v1.13.1: Pulling from supabase/edge-runtime
52d2b7f179e3: Pull complete
bf4f7b8e8bb8: Pull complete
70255be12b95: Pull complete
5fb123420db6: Pull complete
Digest: sha256:e73fe8fb62e31d9ad80bf4e38b3cec21a448a3b9b3da9364a995cc8ace420927
Status: Downloaded newer image for public.ecr.aws/supabase/edge-runtime:v1.13.1
v0.68.0: Pulling from supabase/postgres-meta
1d5252f66ea9: Pull complete
659f9a2fcbfc: Pull complete
c9356b58de51: Pull complete
6663135a74d2: Pull complete
8b36c4cc6f82: Pull complete
69fbdb6b3095: Pull complete
2291d251f078: Pull complete
c9aadcffe9ab: Pull complete
570fe750b6e9: Pull complete
Digest: sha256:31a107dcfe9257792b49f560a5527d5fbd7128b986acad5431b269bac4d17f12
Status: Downloaded newer image for public.ecr.aws/supabase/postgres-meta:v0.68.0
20230803-15c6762: Pulling from supabase/studio
648e0aadf75a: Pull complete
41c739c16d9c: Pull complete
85f19dcf293f: Pull complete
fda13199b871: Pull complete
c66f790f220d: Pull complete
ab6ddbdd32ed: Pull complete
4c5030d6a5f8: Pull complete
3fb02c0ebdcd: Pull complete
ff9a8d9e9990: Pull complete
744fff26449a: Pull complete
Digest: sha256:7bd76dbd9433f0521ef311e5c4b083ed98c549ca08f65222eb33abff64e492a6
Status: Downloaded newer image for public.ecr.aws/supabase/studio:20230803-15c6762
Started supabase local development setup.

         API URL: http://localhost:54321
     GraphQL URL: http://localhost:54321/graphql/v1
          DB URL: postgresql://postgres:postgres@localhost:54322/postgres
      Studio URL: http://localhost:54323
    Inbucket URL: http://localhost:54324
      JWT secret: super-secret-jwt-token-with-at-least-32-characters-long
        anon key: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZS1kZW1vIiwicm9sZSI6ImFub24iLCJleHAiOjE5ODM4MTI5OTZ9.CRXP1A7WOeoJeXxjNni43kdQwgnWNReilDMblYTn_I0
service_role key: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZS1kZW1vIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImV4cCI6MTk4MzgxMjk5Nn0.EGIM96RAZx35lJzdJsyH-qQwv8Hdp7fsn3W0YpN81IU
```

<a href="http://localhost:54323/project/default">http://localhost:54323/project/default</a>

### 1.4 - Profiles Table & RLS

`pnpx supabase migration new profiles`

becomes

`px supabase migration new profiles`

because of

`zsh: command not found: pnpx`

<a href="https://stackoverflow.com/a/70266473">https://stackoverflow.com/a/70266473</a>

<a href="https://pnpm.io/cli/dlx">https://pnpm.io/cli/dlx</a>

in .zshrc

`alias px="pnpm dlx"`

```bash
Packages: +22
++++++++++++++++++++++
Progress: resolved 22, reused 22, downloaded 0, added 22, done
Created new migration at supabase/migrations/20230907075333_profiles.sql.
```

install VS Code extension

"uniquevision.vscode-plpgsql-lsp"

"bradymholt.pgformatter"

user & workbench settings

```json
  // PGFormatter
  "pgFormatter.functionCase": "lowercase",
  "pgFormatter.keywordCase": "lowercase"
```

**supabase/migrations/20230907075333_profiles.sql**

```sql
create table public.profiles(
  id uuid unique references auth.users on delete cascade,
  full_name text,
  updated_at timestamp with time zone default now() not null,
  created_at timestamp with time zone default now() not null,
  primary key (id)
);

alter table public.profiles enable row level security;

create policy "Users can view own profile" on profiles
  for select to authenticated
    using (auth.uid() = id);

create policy "Users can update own profile" on profiles
  for update to authenticated
    using (auth.uid() = id);

create or replace function public.handle_new_user()
  returns trigger
  as $$
begin
  insert into public.profiles(id, full_name)
    values(new.id, new.raw_user_meta_data ->> 'full_name');
  return new;
end;
$$
language plpgsql
security definer;

create trigger on_auth_user_created
  after insert on auth.users for each row
  execute procedure public.handle_new_user();
```

<a href="https://supabase.com/docs/guides/auth/managing-user-data#using-triggers">https://supabase.com/docs/guides/auth/managing-user-data#using-triggers</a>

`px supabase db reset`

```bash
Packages: +22
++++++++++++++++++++++
Progress: resolved 22, reused 22, downloaded 0, added 22, done
Resetting local database...
Restarting containers...
Applying migration 20230907075333_profiles.sql...
Seeding data supabase/seed.sql...
Finished supabase db reset on branch 1.4-Profiles-Table-And-RLS.
```

### 2.1 Server-Side Environment

`p i dotenv`

```bash
Already up to date
Progress: resolved 445, reused 423, downloaded 0, added 0, done
Done in 2.5s
```

**src/lib/server/env.ts**

```ts
import * as dotenv from "dotenv";
dotenv.config();

function getEnvironmentVariable(environmentVariable: string): string {
	const validEnvironmentVariable = process.env[environmentVariable];
	if (!validEnvironmentVariable) {
		throw new Error(`Couldn't find environment variable: ${environmentVariable}`);
	}
	return validEnvironmentVariable;
}

export const ENV = {
	PUBLIC_SUPABASE_ANON_KEY: getEnvironmentVariable("PUBLIC_SUPABASE_ANON_KEY"),
	PUBLIC_SUPABASE_URL: getEnvironmentVariable("PUBLIC_SUPABASE_URL"),
	SUPABASE_SERVICE_ROLE_KEY: getEnvironmentVariable("SUPABASE_SERVICE_ROLE_KEY"),
	SUPABASE_DB_URL: getEnvironmentVariable("SUPABASE_DB_URL")
};
```

### 2.2 - Install Supabase SDKs & Generate Types

`p i @supabase/supabase-js @supabase/auth-helpers-sveltekit`

```bash
Already up to date
Progress: resolved 445, reused 423, downloaded 0, added 0, done
Done in 1.8s
```

`p supabase gen types typescript --local > src/lib/supabase-types.ts`

```bash
v0.60.7: Pulling from supabase/postgres-meta
8740c948ffd4: Pull complete
29fd6e358874: Pull complete
b76523dd8e3e: Pull complete
22a477c2ec9b: Pull complete
9b4ab2388925: Pull complete
949b60406ef6: Pull complete
5e1c3eb6de2b: Pull complete
0a816fedf16c: Pull complete
455915913751: Pull complete
Digest: sha256:c816ae12c3ca785934cf19935c91c08edea6af1488c290fe3b34096e17e23812
Status: Downloaded newer image for public.ecr.aws/supabase/postgres-meta:v0.60.7
(node:1) ExperimentalWarning: Importing JSON modules is an experimental feature. This feature could change at any time
(Use `node --trace-warnings ...` to show where the warning was created)
```

**src/lib/supabase-types.ts**

again

`pnpx`

becomes

`pnpm dlx`

so in the script change it to

```json
"gen:types": "pnpm dlx supabase gen types typescript --local > src/lib/supabase-types.ts && prettier --write src/lib/supabase-types.ts"
```

`p gen:types`

```bash
> modern-saas@0.0.1 gen:types /media/user/d/WWW/modern-saas
> pnpm dlx supabase gen types typescript --local > src/lib/supabase-types.ts && prettier --write src/lib/supabase-types.ts

Progress: resolved 1, reused 0, downloaded 0, added 0
Progress: resolved 19, reused 19, downloaded 0, added 0
Packages: +22
++++++++++++++++++++++
Progress: resolved 22, reused 22, downloaded 0, added 22, done
(node:1) ExperimentalWarning: Importing JSON modules is an experimental feature. This feature could change at any time
(Use `node --trace-warnings ...` to show where the warning was created)
src/lib/supabase-types.ts 242ms
```
