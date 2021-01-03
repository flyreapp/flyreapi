# Flyre API

For more information on using this API, please contact [Daniel Bryant](mailto:bryant.daniel.j@gmail.com?subject=Flyre%20Api%20Info).

## General Usage

Following are some examples in Ruby. They assume you have the library's client code generated and required.

### Creating a User

With an api key in hand, create a user.

```ruby
user = Flyre::Api::Users::Stub.
  new(HOSTNAME, :this_channel_is_insecure).
  create_user(Flyre::Api::CreateUserRequest.new(user: Flyre::Api::User.new),
              metadata: { 'api-key' => API_KEY })
```

### Creating a Token

Create a token to allow your user to access endpoints directly.

```ruby
token = Flyre::Api::Tokens::Stub.
  new(HOSTNAME, :this_channel_is_insecure).
  create_token(Flyre::Api::CreateTokenRequest.new(parent: user.name),
               metadata: { 'api-key' => API_KEY })
```

### Listing Missions

Missions can be accessed with either your api key or a user token.

```ruby
Flyre::Api::Missions::Stub.
  new(HOSTNAME, :this_channel_is_insecure).
  list_missions(Flyre::Api::ListMissionsRequest.new(parent: user.name),
                metadata: { 'api-key' => API_KEY })

Flyre::Api::Missions::Stub.
  new(HOSTNAME, :this_channel_is_insecure).
  list_missions(Flyre::Api::ListMissionsRequest.new(parent: user.name),
                metadata: { 'token' => token.value })
```

### More endpoints

Most endpoints are similar in that they can be accessed in two ways. Users are only able to access their own resources.
Most endpoints are "Standard" with a few "Custom" methods, as defined by [Google's API Design Guide](https://cloud.google.com/apis/design).

## Resources

https://grpc.io/

https://cloud.google.com/apis/design
