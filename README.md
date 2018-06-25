# NAME

MojoX::ConfigAppStart - Start a Mojolicious application with Config::App

# VERSION

version 1.01

[![Build Status](https://travis-ci.org/gryphonshafer/MojoX-ConfigAppStart.svg)](https://travis-ci.org/gryphonshafer/MojoX-ConfigAppStart)
[![Coverage Status](https://coveralls.io/repos/gryphonshafer/MojoX-ConfigAppStart/badge.png)](https://coveralls.io/r/gryphonshafer/MojoX-ConfigAppStart)

# SYNOPSIS

    # look for "mojo_app_lib" value in Config::App configuration
    use MojoX::ConfigAppStart;
    MojoX::ConfigAppStart->start;

    # provide explicit Mojolicious application control library on start call
    use MojoX::ConfigAppStart;
    MojoX::ConfigAppStart->start('Application::Control');

    # provide explicit Mojolicious application control library on use call
    use MojoX::ConfigAppStart 'Application::Control';
    MojoX::ConfigAppStart->start;

# DESCRIPTION

The goal of this module is to provide a simplified way to spin up Mojolicious
applications based on settings from a [Config::App](https://metacpan.org/pod/Config::App) configuration system.

If you have either `MOJO_MODE` or `PLACK_ENV` defined as enviornment
variables, the value will be used as the [Config::App](https://metacpan.org/pod/Config::App) enviornment definition.
If not defined at all, then "development" will be used. What this means in
practice is that from the commandline, calling `morbo` or `hypnotoad`
typically does what you want and expect.

## Effective Equivalence

The following is effectively equivalent to using this module, except that the
`Application::Control` library is derived:

    BEGIN {
        $ENV{CONFIGAPPENV} = $ENV{MOJO_MODE} || $ENV{PLACK_ENV} || 'development';
    }

    use Config::App;
    use Mojolicious::Commands;

    Mojolicious::Commands->start_app('Application::Control');

# METHODS

The following is the only method provided:

## start

The `start()` method calls [Mojolicious::Commands](https://metacpan.org/pod/Mojolicious::Commands)'s `start_app()` and
returns the result.

    MojoX::ConfigAppStart->start;

It can optionally be provided an explicit module name:

    MojoX::ConfigAppStart->start('Application::Control');

# SEE ALSO

You can look for additional information at:

- [GitHub](https://github.com/gryphonshafer/MojoX-ConfigAppStart)
- [CPAN](http://search.cpan.org/dist/MojoX-ConfigAppStart)
- [MetaCPAN](https://metacpan.org/pod/MojoX::ConfigAppStart)
- [AnnoCPAN](http://annocpan.org/dist/MojoX-ConfigAppStart)
- [Travis CI](https://travis-ci.org/gryphonshafer/MojoX-ConfigAppStart)
- [Coveralls](https://coveralls.io/r/gryphonshafer/MojoX-ConfigAppStart)
- [CPANTS](http://cpants.cpanauthors.org/dist/MojoX-ConfigAppStart)
- [CPAN Testers](http://www.cpantesters.org/distro/G/MojoX-ConfigAppStart.html)

# AUTHOR

Gryphon Shafer <gryphon@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2018 by Gryphon Shafer.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
