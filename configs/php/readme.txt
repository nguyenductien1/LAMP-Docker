docker run -it --rm -v /mycode/:/home/  php:7.3-fpm cp /usr/local/etc/php/php.ini-production /home/php.ini


//
short_open_tag = On
expose_php = Off

; THIẾT LẬP PHP SESSION DÙNG MEMCACHED
session.save_handler = memcached
session.save_path = "c-memcached01:11211"
memcached.sess_locking = 0
memcached.sess_prefix = 'memc.sess.'

; THIẾT LẬP OPCACHE NẾU CÓ DÙNG (cache mã nguồn PHP)
; zend_extension=opcache.so;
; opcache.interned_strings_buffer=4
; opcache.max_accelerated_files=2000
; opcache.memory_consumption=64
; opcache.revalidate_freq=2
; opcache.fast_shutdown=0
; opcache.enable_cli=0
; opcache.interned_strings_buffer=4
; opcache.max_accelerated_files=2000
; opcache.memory_consumption=64
; opcache.revalidate_freq=2
; opcache.fast_shutdown=0
; opcache.enable_cli=0

docker build -t php:version2 --force-rm -f Dockerfile .    # tạo image từ Dockerfile
docker save --output php.tar php:version2                  # lưu image ra file (để gộp layer)
docker image rm php:version2                               # xóa image
docker load -i php.tar                                     # nạp lại image từ file