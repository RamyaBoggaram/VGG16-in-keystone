{\rtf1\ansi\ansicpg1252\cocoartf2709
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;\red22\green21\blue22;\red246\green246\blue246;\red18\green79\blue146;
}
{\*\expandedcolortbl;;\cssrgb\c11373\c10980\c11373;\cssrgb\c97255\c97255\c97255;\cssrgb\c7059\c39216\c63922;
}
\paperw11900\paperh16840\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\deftab720
\pard\pardeftab720\partightenfactor0

\f0\fs30 \cf2 \cb3 \expnd0\expndtw0\kerning0
set(eapp_bin hello)\cb1 \
\cb3 set(eapp_src eapp/tinyNN-predict.c)\cb1 \
\cb3 set(host_bin hello-runner)\cb1 \
\cb3 set(host_src host/host.cpp)\cb1 \
\cb3 set(package_name "{\field{\*\fldinst{HYPERLINK "http://hello.ke/"}}{\fldrslt \cf4 hello.ke}}")\cb1 \
\cb3 set(package_script "./hello-runner hello eyrie-rt")\cb1 \
\
\cb3 if(RISCV32)\cb1 \
\cb3 \'a0\'a0set(eyrie_plugins "freemem io_syscall linux_syscall env_setup rv32")\cb1 \
\cb3 else()\cb1 \
\cb3 \'a0\'a0set(eyrie_plugins "freemem io_syscall linux_syscall env_setup")\cb1 \
\cb3 endif()\cb1 \
\
\cb3 # eapp\cb1 \
\
\cb3 add_executable($\{eapp_bin\} $\{eapp_src\})\cb1 \
\cb3 target_link_libraries($\{eapp_bin\} "-static")\cb1 \
\
\cb3 # host\cb1 \
\
\cb3 add_executable($\{host_bin\} $\{host_src\})\cb1 \
\cb3 target_link_libraries($\{host_bin\} $\{KEYSTONE_LIB_HOST\} $\{KEYSTONE_LIB_EDGE\})\cb1 \
\
\cb3 # add target for Eyrie runtime (see keystone.cmake)\cb1 \
\
\cb3 set(eyrie_files_to_copy .options_log eyrie-rt)\cb1 \
\cb3 add_eyrie_runtime($\{eapp_bin\}-eyrie\cb1 \
\cb3 \'a0\'a0$\{eyrie_plugins\}\cb1 \
\cb3 \'a0\'a0$\{eyrie_files_to_copy\})\cb1 \
\
\cb3 # add target for packaging (see keystone.cmake)\cb1 \
\
\cb3 add_keystone_package($\{eapp_bin\}-package\cb1 \
\cb3 \'a0\'a0$\{package_name\}\cb1 \
\cb3 \'a0\'a0$\{package_script\}\cb1 \
\cb3 \'a0\'a0$\{eyrie_files_to_copy\} $\{eapp_bin\} $\{host_bin\})\cb1 \
\
\cb3 add_dependencies($\{eapp_bin\}-package $\{eapp_bin\}-eyrie)\cb1 \
\
\cb3 # add package to the top-level target\cb1 \
\cb3 add_dependencies(examples $\{eapp_bin\}-package)}