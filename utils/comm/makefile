### loyangliu created ###

################## complie files ##################
OUTPUTDIR := output
EXECUTABLE := $(OUTPUTDIR)/libutilcomm.so
## ��ָ̬����������.cpp/.o/.d�ļ�λ�ã��ʲ���ҪVPATH��vpath
SOURCE := $(notdir $(wildcard *.c *.cc) $(shell echo *.cpp))
OBJS := $(addprefix $(OUTPUTDIR)/,$(patsubst %.cpp,%.o,$(patsubst %.c,%.o,$(patsubst %.cc,%.o,$(SOURCE)))))
DEPS := $(patsubst %.o,%.d,$(OBJS))
INCLUDE :=
LIBS :=
CXXFLAGS := -std=c++11 -g

##ָ��Ŀ�����������ļ�����λ��
VPATH :=

everything:prepare $(EXECUTABLE)

prepare:
	@if [ ! -e $(OUTPUTDIR) ]; then \
	mkdir $(OUTPUTDIR); chmod 777 $(OUTPUTDIR); \
	fi

$(OUTPUTDIR)/%.d:%.cpp
	@[ -e $(OUTPUTDIR) ] || mkdir $(OUTPUTDIR) && chmod 777 $(OUTPUTDIR)
	@g++ $(INCLUDE) $(CXXFLAGS) -MM -MD -o $@ $<
	@echo "generate $< ==> $@"
	@sed -i '1,1s/^/$(OUTPUTDIR)\//g' $@

$(OUTPUTDIR)/%.d:%.cc
	@[ -e $(OUTPUTDIR) ] || mkdir $(OUTPUTDIR) && chmod 777 $(OUTPUTDIR)
	@g++ $(INCLUDE) $(CXXFLAGS) -MM -MD -o $@ $<
	@echo "generate $< ==> $@"
	@sed -i '1s/^/$(OUTPUTDIR)\//g' $@

$(EXECUTABLE):$(OBJS)
	@g++ $(CXXFLAGS) $(INCLUDE) -shared -fpic -o $@ $^ $(LIBS)
	@cp $@ ../../bin

$(OUTPUTDIR)/%.o:
	@g++ $(CXXFLAGS) $(INCLUDE) -fPIC -o $@ -c $<
	@echo "compile $^ ==> $@"


##���Զ����ɵ�Ŀ���ļ���������ϵ��������
## tips: makefile��include�ĵ��÷�ʽ
## 1���ȵ�ָ����Ŀ¼���������õ��ļ���
## 2�����û���ҵ������make��-Iָ����Ŀ¼���ң������û�ҵ������'/usr/local/include'��Ŀ¼����
## 3��������ջ���û���ҵ�����makefile����ͼѰ��ƥ����������ɶ�Ӧ�ļ������籾����%.d:%.cpp
sinclude $(DEPS)

clean:
	@rm -rf $(OUTPUTDIR)
	@rm -rf *.bak