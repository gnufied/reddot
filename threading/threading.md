!SLIDE
# Threading #

!SLIDE
# Ruby 1.8 had green threads #

!SLIDE smaller
# In MRI 1.8, all blocking calls are turned into non-blocking calls internally.#


!SLIDE smaller

    @@@ c
        fd = fileno(fptr->f);
        str = rb_tainted_str_new(0, buflen);
    retry:
        rb_str_locktmp(str);
        rb_thread_wait_fd(fd); // will call rb_thread_schedule
        TRAP_BEG;
        slen = recvfrom(fd, RSTRING(str)->ptr, buflen, flags, 
          (struct sockaddr*)buf, &alen);
        TRAP_END;
        rb_str_unlocktmp(str);
	
    

!SLIDE

# 1.9 has native threads with GVL #

!SLIDE smaller
    @@@ c
    // socket.c
    #define BLOCKING_REGION(func, arg) 
       (long)rb_thread_blocking_region((func),(arg), 
         RUBY_UBF_IO, 0)
       
    // Blocking call for IO   
    BLOCKING_REGION(recvfrom_blocking, &arg)) < 0)

    // thread.c
    //
    VALUE rb_thread_blocking_region(
         rb_blocking_function_t *func,
         void *data1,rb_unblock_function_t *ubf, 
         void *data2)


!SLIDE 
# 1.9.3 introduced queuing GVL #

!SLIDE smaller
# Wake-up queued threads.The wake-up order is simple FIFO #



