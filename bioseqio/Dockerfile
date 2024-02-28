FROM perl:5.39.8

RUN cpanm IPC::System::Simple DateTime::Locale DateTime Dist::Zilla Moose Text::CSV ExtUtils::MakeMaker Getopt::Long Try::Tiny Exception::Class

RUN cpanm Dist::Zilla::Plugin::AutoPrereqs Dist::Zilla::Plugin::Encoding Dist::Zilla::Plugin::FileFinder::ByName Dist::Zilla::Plugin::MetaResources Dist::Zilla::Plugin::PkgVersion Dist::Zilla::Plugin::PodWeaver Dist::Zilla::Plugin::RequiresExternal Dist::Zilla::Plugin::RunExtraTests Dist::Zilla::PluginBundle::Git Dist::Zilla::PluginBundle::Starter

RUN cpanm --force XML::DOM::XPath

RUN cpanm --force Bio::Seq Bio::SeqIO
