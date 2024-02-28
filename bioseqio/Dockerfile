FROM ubuntu:22.04

RUN apt-get update && \
    apt-get install -y procps libcurl4-openssl-dev libssl-dev perl cpanminus zlib1g-dev cpanminus gcc \
    libncurses5-dev libncursesw5-dev libssl-dev libxml-libxml-perl libgd-gd2-perl locales git && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN cpanm IPC::System::Simple DateTime::Locale DateTime Dist::Zilla Moose Text::CSV ExtUtils::MakeMaker Getopt::Long Try::Tiny Exception::Class

RUN cpanm Dist::Zilla::Plugin::AutoPrereqs Dist::Zilla::Plugin::Encoding Dist::Zilla::Plugin::FileFinder::ByName Dist::Zilla::Plugin::MetaResources Dist::Zilla::Plugin::PkgVersion Dist::Zilla::Plugin::PodWeaver Dist::Zilla::Plugin::RequiresExternal Dist::Zilla::Plugin::RunExtraTests Dist::Zilla::PluginBundle::Git Dist::Zilla::PluginBundle::Starter

RUN cpanm --force XML::DOM::XPath

RUN cpanm --force Bio::Seq Bio::SeqIO
