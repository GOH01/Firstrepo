#include<stdio.h>
#include<winsock2.h>
#pragma comment (lib,"ws2_32");

int main(void)
{
	WSADATA wsaData;
	SOCKET hServSock, hClntSock;
	SOCKADDR_IN servAddr, clntAddr;
	char rcvMsg[100] = { 0 };
	int strLen;
	int szClntAddr;

	while (1)
	{
		if (WSAStartup(MAKEWORD(2, 2), &wsaData) != 0)
		{
			printf("WSAStartup() error!");
		}
		hServSock = socket(PF_INET, SOCK_STREAM, 0);
		if (hServSock == INVALID_SOCKET)
		{
			printf("socket() error!");
		}
		memset(&servAddr, 0, sizeof(servAddr));
		servAddr.sin_family = AF_INET;
		servAddr.sin_addr.s_addr = htonl(INADDR_ANY);
		servAddr.sin_addr.s_addr = htonl(INADDR_ANY);
		servAddr.sin_port = htons(1234);

		if (bind(hServSock, (SOCKADDR*)&servAddr, sizeof(servAddr)) == SOCKET_ERROR)
		{
			printf("bind() error");
		}
		if (listen(hServSock, 5) == SOCKET_ERROR)
		{
			printf("listen() error");
		}

		printf("서버 수신 대기중..\n");
		szClntAddr = sizeof(clntAddr);
		hClntSock = accept(hServSock, (SOCKADDR*)&clntAddr, &szClntAddr);
		if (hClntSock == INVALID_SOCKET)
		{
			printf("accept() error");
		}
		strLen = recv(hClntSock, rcvMsg, sizeof(rcvMsg) - 1, 0);
		printf("Message from Client: %s\n", rcvMsg);

		closesocket(hClntSock);
		closesocket(hServSock);
		WSACleanup();

	}
	return 0;
}
