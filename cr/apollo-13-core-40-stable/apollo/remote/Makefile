CC= arm-linux-gnueabihf-gcc
CXX= arm-linux-gnueabihf-g++
LDFLAGS= -lgcc -lc -lgcc -lsupc++ -lstdc++ -static -pthread -Wl,--no-as-needed -Wl,--whole-archive -lpthread -Wl,--no-whole-archive
CXXFLAGS= -I ../.. -std=c++11 -mfloat-abi=soft

all: libremote.a remote

remote: main.o libremote.a
	$(CXX) $(CXXFLAGS) main.o -o $@ $(LDFLAGS) -L. -lremote

main.o: main.cc packet_manager.h network_packet.h
	$(CXX) -c $(CXXFLAGS) $< -o $@

packet_manager.o: packet_manager.cc packet_manager.h network_packet.h
	$(CXX) -c $(CXXFLAGS) $< -o $@

connection_manager.o: connection_manager.cc connection_manager.h
	$(CXX) -c $(CXXFLAGS) $< -o $@

libremote.a: packet_manager.o connection_manager.o ../core/safe_exit.o ../core/serial.o
	ar -r $@ $^

.PHONY: clean

clean:
	rm -rf *.o *.a remote
