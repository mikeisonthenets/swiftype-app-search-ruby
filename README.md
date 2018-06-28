# Ruby client for the Swiftype App Search API

## Installation

To install the gem, execute:

```bash
gem install swiftype-app-search
```

Or place `gem 'swiftype-app-search', '~> 0.1.3` in your `Gemfile` and run `bundle install`.

## Usage

### Setup: Configuring the client and authentication

Create a new instance of the Swiftype App Search Client. This requires your `[HOST_IDENTIFIER]`, which
identifies the unique hostname of the Swiftype API that is associated with your Swiftype account.
It also requires a valid `[PRIVATE_KEY]`, which authenticates requests to the API. You can find both of these within
the [Credentials](https://app.swiftype.com/as/credentials) menu:

```ruby
client = SwiftypeAppSearch::Client.new(:host_identifier => 'host-c5s2mj', :private_key => 'api-mu75psc5egt9ppzuycnc2mc3')
```

### API Methods

This client is a thin interface to the Swiftype App Search Api. Additional details for requests and responses can be
found in the [documentation](https://swiftype.com/documentation/app-search).

#### Indexing: Creating or Updating a Single Document

```ruby
engine_name = 'favorite-videos'
document = {
  :id => 'INscMGmhmX4',
  :url => 'https://www.youtube.com/watch?v=INscMGmhmX4',
  :title => 'The Original Grumpy Cat',
  :body => 'A wonderful video of a magnificent cat.'
}

begin
  response = client.index_document(engine_name, document)
  puts response
rescue SwiftypeAppSearch::ClientException => e
  puts e
end
```

#### Indexing: Creating or Updating Documents

```ruby
engine_name = 'favorite-videos'
documents = [
  {
    :id => 'INscMGmhmX4',
    :url => 'https://www.youtube.com/watch?v=INscMGmhmX4',
    :title => 'The Original Grumpy Cat',
    :body => 'A wonderful video of a magnificent cat.'
  },
  {
    :id => 'JNDFojsd02',
    :url => 'https://www.youtube.com/watch?v=dQw4w9WgXcQ',
    :title => 'Another Grumpy Cat',
    :body => 'A great video of another cool cat.'
  }
]

begin
  response = client.index_documents(engine_name, documents)
  puts response
rescue SwiftypeAppSearch::ClientException => e
  puts e
end
```

#### Listing Documents

```ruby
engine_name = 'favorite-videos'
document_ids = ['INscMGmhmX4', 'JNDFojsd02']

begin
  response = client.get_documents(engine_name, document_ids)
  puts response
rescue SwiftypeAppSearch::ClientException => e
  puts e
end
```

#### Destroying Documents

```ruby
engine_name = 'favorite-videos'
document_ids = ['INscMGmhmX4', 'JNDFojsd02']

begin
  response = client.destroy_documents(engine_name, document_ids)
  puts response
rescue SwiftypeAppSearch::ClientException => e
  puts e
end
```

#### Listing Engines

```ruby
begin
  response = client.list_engines
  puts response
rescue SwiftypeAppSearch::ClientException => e
  puts e
end
```

#### Retrieving Engines

```ruby
engine_name = 'favorite-videos'

begin
  response = client.get_engine(engine_name)
  puts response
rescue SwiftypeAppSearch::ClientException => e
  puts e
end
```

#### Creating Engines

```ruby
engine_name = 'favorite-videos'

begin
  response = client.create_engine(engine_name)
  puts response
rescue SwiftypeAppSearch::ClientException => e
  puts e
end
```

#### Destroying Engines

```ruby
engine_name = 'favorite-videos'

begin
  response = client.destroy_engine(engine_name)
  puts response
rescue SwiftypeAppSearch::ClientException => e
  puts e
end
```

#### Searching

```ruby
engine_name = 'favorite-videos'
query = 'cat'
search_fields = { :title => {} }
result_fields = { :title => { :raw => {} } }
options = { :search_fields => search_fields, :result_fields => result_fields }

begin
  response = client.search(engine_name, query, options)
  puts response
rescue SwiftypeAppSearch::ClientException => e
  puts e
end
```

## Running Tests

```bash
export PRIVATE_KEY="[AS_PRIVATE_KEY]"
export HOST_IDENTIFIER="[AS_HOST_IDENTIFIER]"
bundle exec rspec
```

You can also run tests against a local environment by passing a `AS_API_ENDPOINT` environment variable

```bash
export API_KEY="[AS_PRIVATE_KEY]"
export API_ENDPOINT="http://[AS_HOST_IDENTIFIER].api.127.0.0.1.ip.es.io:3002/api/as/v1"
bundle exec rspec
```

## Debugging API calls

If you need to debug an API call made by the client, there are a few things you could do:

1. Setting `AS_DEBUG` environment variable to `true` would enable HTTP-level debugging and you would
   see all requests generated by the client on your console.

2. You could use our API logs feature in App Search console to see your requests and responses live.

3. In your debug logs you could find a `X-Request-Id` header value. That could be used when talking
   to Swiftype Customer Support to help us quickly find your API request and help you troubleshoot
   your issues.

## Contributions

To contribute code, please fork the repository and submit a pull request.
