
[![Gem Version](https://badge.fury.io/rb/sensu-plugins-oracle.svg)](https://badge.fury.io/rb/sensu-plugins-oracle)
[![Maintainability](https://api.codeclimate.com/v1/badges/a96aadf931c023673c49/maintainability)](https://codeclimate.com/github/thomis/sensu-plugins-oracle/maintainability)
[![Build Status](https://travis-ci.org/thomis/sensu-plugins-oracle.svg?branch=master)](https://travis-ci.org/thomis/sensu-plugins-oracle)

# sensu-plugins-oracle

This sensu plugin provides native Oracle instrumentation.

## Files
  * bin/check-oracle-alive.rb
  * bin/check-oracle-query.rb

## Usage

  ```
  -- check a single connection
  check-oracle-alive.rb -u scott -p tiger -d hr

  -- check a single connection with timeout
  check-oracle-alive.rb -u scott -p tiger -d hr -T 30
  ```

  ```
  -- check multiple connections as defined in a file, use 5 worker threads (-W 5) and verbose output (-v)
  check-oracle-alive.rb -f connections.csv -W 5 -v

  > cat connections.csv
    # production connection
    example_connection_1,scott/tiger@hr

    # test connection
    example_connection_2,scott/tiger@hr_test
  ```

  ```
  -- check for invalid objects in a schema, shows type and name if there are invalid objects (-s), define a ciritical boundary only (-c)
  check-oracle-query.rb -u scott -p tiger -d hr -t -s -query "select object_type, object_name from user_objects where status = 'INVALID'" -c "value > 0"

  -- same as above but check for all connections in a file, use 5 worker threads
  check-oracle-query.rb -f connections.csv -t -s -query "select object_type, object_name from user_objects where status = 'INVALID'" -c "value > 0" -W 5

  ```

## Installation

[Installation and Setup](http://sensu-plugins.io/docs/installation_instructions.html)
