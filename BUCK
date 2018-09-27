# cxx_library(
#   name = 'foo', 
#   header_namespace = '', 
#   exported_headers = {
#     'foo.hpp': 'include/foo.hpp', 
#   }, 
#   srcs = [
#     'src/foo.cpp', 
#   ], 
# )

cxx_genrule(
  name = 'foo-lib', 
  out = 'foo.a', 
  srcs = [
    'include/foo.hpp', 
    'src/foo.cpp', 
  ], 
  cmd = '$(cxx) -c -I./include ./src/foo.cpp -static -o $OUT', 
)

prebuilt_cxx_library(
  name = 'foo-headers', 
  header_only = True, 
  header_namespace = '', 
  exported_headers = {
    'foo.hpp': 'include/foo.hpp', 
  }, 
)

prebuilt_cxx_library(
  name = 'foo', 
  platform_static_lib = [
    ('^linux.*', ':foo-lib'), 
  ], 
  deps = [
    ':foo-headers', 
  ], 
)

cxx_binary(
  name = 'app', 
  header_namespace = '', 
  srcs = [
    'src/app.cpp', 
  ], 
  deps = [
    ':foo', 
  ], 
)
