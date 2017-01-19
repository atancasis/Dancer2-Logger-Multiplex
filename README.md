# NAME

Dancer2::Logger::Multiplex - Log to multiple Dancer2::Logger engines

# VERSION

version 0.01

# SYNOPSIS

    use Dancer2::Logger::Multiplex;

# DESCRIPTION

Implements a multiplexing logger engine to dispatch logs to multiple
backend [Dancer2::Core::Role::Logger](https://metacpan.org/pod/Dancer2::Core::Role::Logger) engines.

# METHODS

## log($level, $message)

Writes the log message to multiple logger engines.

# CONFIGURATION

The setting **logger** should be set to `Multiplex` in order to use this
logging engine in a Dancer2 application.

Below is a sample configuration:

    logger: "Multiplex"

    engines:
      logger:
        Multiplex:
          loggers:
            - Console
            - File
            - Fluent
        File:
          log_dir: "/var/log/myapp"
          file_name: "myapp.log"
        Fluent:
          tag_prefix: "myapp"
          host: "127.0.0.1"
          port: 24224

Allowed options are as follows:

- loggers

    Specifies the list of [Dancer2::Core::Role::Logger](https://metacpan.org/pod/Dancer2::Core::Role::Logger) backend engines to
    dispatch log messages to.

    Each logger engine will be initialized with their corresponding
    configurations. As such, in the example above, [Dancer2::Logger::File](https://metacpan.org/pod/Dancer2::Logger::File)
    will be initialized with settings for _log\_dir_ and _file\_name_, while
    [Dancer2::Logger::Fluent](https://metacpan.org/pod/Dancer2::Logger::Fluent) will be initialized with settings for
    _tag\_prefix_, _host_, and _port_ as specified in the sample configuration.

# AUTHOR

Arnold Tan Casis <atancasis@cpan.org>

# COPYRIGHT

Copyright 2017- Arnold Tan Casis

# LICENSE

This library is free software; you can redistribute it and/or modify it
under the same terms as Perl itself.

# SEE ALSO

See [Dancer2](https://metacpan.org/pod/Dancer2) for details about logging in route handlers.
