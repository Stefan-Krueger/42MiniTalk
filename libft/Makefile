# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Makefile                                           :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: skrueger <skrueger@student.42heilbronn.    +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2021/06/22 14:01:42 by skrueger          #+#    #+#              #
#    Updated: 2022/02/20 15:27:57 by skrueger         ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

NAME = libft.a

HEADER = libft.h

COMPILER = gcc

CFLAGS = -Wall -Wextra -Werror

SRC				=	ft_atoi.c \
					ft_putchar_fd.c \
					ft_putnbr_fd.c \
					ft_putstr_fd.c \
					ft_strlen.c \

OBJ				= $(SRC:.c=.o)

all:			$(NAME)

$(NAME):		$(SRC)
				$(COMPILER) $(CFLAGS) -c $(SRC)
				ar -crs $(NAME) $(OBJ)

clean:
	rm -f *.o

fclean:	clean
	rm -f $(NAME)

re:	fclean all