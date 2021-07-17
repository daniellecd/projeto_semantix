### Etapas para instalação no Windows 10

 1. Verificar o OS build (Windows/System/Settings/About). Caso seja inferior a 18362 precisa atualizar [Windows 10](https://www.microsoft.com/pt-br/software-download/windows10) (20.04) - Clicar em atualizar agora
    
 2. Pesquisar por **Recursos** (Ativar ou desativar recursos do Windows)
    
	 - Desativar Hyper-V
	 - Desativar Plataforma do Hipervisor do Windows
	 - Habilitar a Plataforma de Máquina Virtual
	 - Habilitar o Subsistema do Windows para Linux (WSL)
        
3.  Fazer download e instalar o [WSL 2](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi).
    
4.  Definir o WSL como padrão via Power Shell (como administrador) `wsl --set-default-version 2`
    
5.  Fazer download e instalar uma distribuição Linux disponível na Microsoft Store, sendo recomendado o Ubuntu 20.04 LTS
    
6.  Fazer download e instalar o [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows/) - Clicar em Get Docker.
    
    - Abrir o programa e verificar se em _Settings - Resource - WSL Integration_ - estão habilitados o "Enable integration with my default WSL distro" e "Ubuntu-20.04"

------------
<h5 align="center"> Feito com ❤  by daniellecd
</h5>


