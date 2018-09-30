project(
	'rSON',
	['c', 'cpp'],
	default_options: [
		'cpp_std=c++14',
		'warning_level=3',
		'b_pch=false'
	],
	version: '0.3.1'
)

cxx = meson.get_compiler('cpp')
pkgconfig = import('pkgconfig')

if target_machine.system() != 'windows'
	add_project_link_arguments('-z', 'defs', language: 'cpp')
endif

rSONSrc = [
	'JSONErrors.cpp', 'JSONAtom.cpp', 'JSONNull.cpp', 'JSONBool.cpp',
	'JSONInt.cpp', 'JSONFloat.cpp', 'JSONString.cpp', 'JSONObject.cpp',
	'JSONArray.cpp', 'String.cpp', 'Stream.cpp', 'Parser.cpp',
	'Writer.cpp'
]

rSONSocketSrc = ['rSON_socket.cpp']

rSON = library(
	'rSON',
	rSONSrc,
	cpp_args: ['-D__rSON__'],
	version: meson.project_version(),
	install: true
)

rSONSocket = library(
	'rSON.socket',
	rSONSocketSrc,
	link_with: [rSON],
	version: meson.project_version(),
	install: true
)

pkgconfig.generate(
	name: 'rSON',
	filebase: 'rSON',
	libraries: rSON,
	version: meson.project_version(),
	description: 'A simple but effective JSON parser for C++'
)

pkgconfig.generate(
	name: 'rSON Socket',
	filebase: 'rSON_socket',
	libraries: [rSONSocket, rSON],
	version: meson.project_version(),
	description: 'Sockets handling for rSON, a simple but effective JSON parser for C++'
)