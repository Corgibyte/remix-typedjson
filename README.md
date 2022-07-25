# remix-typedjson

<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->

[![All Contributors](https://img.shields.io/badge/all_contributors-2-orange.svg?style=flat-square)](#contributors-)

<!-- ALL-CONTRIBUTORS-BADGE:END -->

This package is a replacement for [`superjson`](https://github.com/blitz-js/superjson) to use in your Remix app. It handles a subset
of types that `superjson` supports, but is faster and smaller.

Example site: https://remix-typedjson-example-production.up.railway.app/

Example repo: https://github.com/kiliman/remix-typedjson-example

The following types are supported:

- `Date`
- `BigInt`
- `Set`
- `Map`
- `RegExp`
- `undefined`
- `Error`
- `NaN`
- `Number.POSITIVE_INFINITY`
- `Number.NEGATIVE_INFINITY`

# 🚧 Work In Progress

Sets and Maps currently only support string keys and JSON serializable values. Complex types coming soon.

# 🛠 How to Use with Remix

In order to get full-type fidelity and type inference, you must be on Remix
v1.6.5+. You will also need to import the following replacement functions.

## `typedjson`

Replacement for Remix `json` helper. It also supports the optional `Response Init`, so you can return headers, etc.

Make sure your `loader` and `action` use the new declaration format:

```js
❌ export const loader: LoaderFunction = async ({request}) => {}
✅ export const loader = async ({request}: LoaderArgs) => {}
✅ export async function loader({request}: LoaderArgs) {}
```

### Usage

```js
return typedjson(
  { greeting: 'hello', today: new Date() },
  { headers: { 'set-header': await commitSession(session) } },
)
```

## `useTypedLoaderData`

Replacement for Remix `useLoaderData`. Use the generic `<typeof loader>` to
get the correct type inference.

### Usage

```js
const loaderData = useTypedLoaderData<typeof loader>()
```

## `useTypedActionData`

Replacement for Remix `useActionData`. Use the generic `<typeof action>` to
get the correct type inference.

### Usage

```js
const actionData = useTypedActionData<typeof action>()
```

## `useTypedFetcher`

Replacement for Remix `useFetcher`. Use the generic `<typeof loader|action>` to
get the correct type inference for the `fetcher.data` property.

### Usage

```js
const fetcher = useTypedFetcher<typeof action>()
fetcher.data // data property is fully typed
```

## `redirect`

In order to return a `redirect`, you will need to import the `redirect` function from this package, in order for the type inference to work properly.

However, you can also `throw redirect()` and you can use the original `redirect` function from Remix.

## 😍 Contributors

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://kiliman.dev/"><img src="https://avatars.githubusercontent.com/u/47168?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Kiliman</b></sub></a><br /><a href="https://github.com/Kiliman/remix-typedjson/commits?author=kiliman" title="Code">💻</a> <a href="https://github.com/Kiliman/remix-typedjson/commits?author=kiliman" title="Documentation">📖</a></td>
    <td align="center"><a href="https://kentcdodds.com/"><img src="https://avatars.githubusercontent.com/u/1500684?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Kent C. Dodds</b></sub></a><br /><a href="https://github.com/Kiliman/remix-typedjson/commits?author=kentcdodds" title="Code">💻</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
