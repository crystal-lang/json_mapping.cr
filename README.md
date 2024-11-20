> [!IMPORTANT]
> This library is no longer supported or updated by the Crystal Team,
> therefore we have archived the repository.
> 
> The contents are still available readonly and continue to work as a
> [shards](https://github.com/crystal-lang/shards/) dependency.
>
> If you wish to continue development yourself, we recommend you fork it.
> We can also arrange to transfer ownership.
>
> If you have further question, please ask on https://forum.crystal-lang.org

# json_mapping

Provides the legacy `JSON.mapping` macro method.

This shard is provided as-is and considered deprecated. It won't receive feature enhancements.

Please consider using [`JSON::Serializable`](https://crystal-lang.org/api/latest/JSON/Serializable.html) instead, the successor included in Crystal's standard library.

## Installation

1. Add the dependency to your `shard.yml`:

```yaml
dependencies:
  json_mapping:
    github: crystal-lang/json_mapping.cr
```

2. Run `shards install`

## Usage

```crystal
require "json_mapping"

class Location
  JSON.mapping(
    lat: Float64,
    lng: Float64,
  )
end

class House
  JSON.mapping(
    address: String,
    location: {type: Location, nilable: true},
  )
end

house = House.from_json(%({"address": "Crystal Road 1234", "location": {"lat": 12.3, "lng": 34.5}}))
house.address  # => "Crystal Road 1234"
house.location # => #<Location:0x10cd93d80 @lat=12.3, @lng=34.5>
house.to_json  # => %({"address":"Crystal Road 1234","location":{"lat":12.3,"lng":34.5}})

houses = Array(House).from_json(%([{"address": "Crystal Road 1234", "location": {"lat": 12.3, "lng": 34.5}}]))
houses.size    # => 1
houses.to_json # => %([{"address":"Crystal Road 1234","location":{"lat":12.3,"lng":34.5}}])
```
